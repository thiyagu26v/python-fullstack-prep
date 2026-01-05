---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# Django & DRF Live-Task Mastery - Level 2 (Advanced)

This document covers advanced Django scenarios and Django Rest Framework (DRF) tasks often found in senior-level or high-growth startup interviews.

---

## **Section 1: DRF Serializers (Q26-30)**

### **26. Create a basic ModelSerializer for a Product**
**Task:** Expose the `id`, `name`, and `price` of the `Product` model via DRF.

#### **Solution:**
```python
from rest_framework import serializers
from .models import Product

class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ['id', 'name', 'price'] # Only expose specific fields
```

---

### **27. Add a custom calculated field using SerializerMethodField**
**Task:** Add a `taxed_price` field to the serializer that returns the price + 18% GST.

#### **Solution:**
```python
class ProductSerializer(serializers.ModelSerializer):
    taxed_price = serializers.SerializerMethodField() # Custom read-only field

    class Meta:
        model = Product
        fields = ['id', 'name', 'price', 'taxed_price']

    def get_taxed_price(self, obj): # Pattern: get_<fieldname>
        return obj.price * 1.18 # Add 18% tax to the original price
```

---

### **28. Implement Nested Serializers (Parent -> Child)**
**Task:** For a `Category` model, show all related `Product` items in the JSON response.

#### **Solution:**
```python
class CategorySerializer(serializers.ModelSerializer):
    products = ProductSerializer(many=True, read_only=True) # Many=True for lists

    class Meta:
        model = Category
        fields = ['id', 'name', 'products']
```

---

### **29. Validate data inside a Serializer**
**Task:** Ensure the `name` field in a `ProductSerializer` has at least 5 characters.

#### **Solution:**
```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = '__all__'

    def validate_name(self, value): # Field-level validation
        if len(value) < 5:
            raise serializers.ValidationError("Name is too short!")
        return value
```

---

### **30. Override create() for custom logic in Serializer**
**Task:** When creating a `Comment`, automatically set the `ip_address` from the request.

#### **Solution:**
```python
class CommentSerializer(serializers.ModelSerializer):
    class Meta:
        model = Comment
        fields = ['body']

    def create(self, validated_data):
        # Accessing request from context passed by the view
        validated_data['ip_address'] = self.context['request'].META.get('REMOTE_ADDR')
        return super().create(validated_data)
```

---

## **Section 2: API Views & ViewSets (Q31-40)**

### **31. Create a function-based API view (@api_view)**
**Task:** Create a simple endpoint that returns {"message": "Hello"}.

#### **Solution:**
```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['GET']) # Restricts to GET requests
def hello_api(request):
    return Response({"message": "Hello"}) # Returns JSON automatically
```

---

### **32. Use a Class-Based APIView**
**Task:** Implement a shared endpoint that handles GET (list) and POST (create).

#### **Solution:**
```python
from rest_framework.views import APIView
from rest_framework import status

class ProductAPI(APIView):
    def get(self, request):
        products = Product.objects.all()
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = ProductSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```

---

### **33. Faster development with Generic API Views**
**Task:** Create a list-and-create view using only 3 lines of code.

#### **Solution:**
```python
from rest_framework import generics

class ProductListCreate(generics.ListCreateAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

---

### **34. Full CRUD in one class (ModelViewSet)**
**Task:** Implement List, Create, Retrieve, Update, and Delete for `Order`.

#### **Solution:**
```python
from rest_framework import viewsets

class OrderViewSet(viewsets.ModelViewSet):
    queryset = Order.objects.all()
    serializer_class = OrderSerializer

# In urls.py: router.register(r'orders', OrderViewSet)
```

---

### **35. Add a custom @action to a ViewSet**
**Task:** Add a `cancel` endpoint (e.g., `/orders/1/cancel/`) to the Order ViewSet.

#### **Solution:**
```python
from rest_framework.decorators import action

class OrderViewSet(viewsets.ModelViewSet):
    # ... existing code ...

    @action(detail=True, methods=['post']) # detail=True means it needs an ID
    def cancel(self, request, pk=None):
        order = self.get_object()
        order.status = 'Cancelled'
        order.save()
        return Response({'status': 'order cancelled'})
```

---

### **36. Implement Token Authentication**
**Task:** Protect an API so only users with a valid token can access it.

#### **Solution:**
```python
from rest_framework.permissions import IsAuthenticated
from rest_framework.authentication import TokenAuthentication

class PrivateDataView(APIView):
    authentication_classes = [TokenAuthentication] # How to identify user
    permission_classes = [IsAuthenticated]     # What to check

    def get(self, request):
        return Response({"secret": "42"})
```

---

### **37. Custom Permission: IsOwnerOrReadOnly**
**Task:** Allow Anyone to see a post, but only the owner can edit/delete it.

#### **Solution:**
```python
from rest_framework import permissions

class IsOwnerOrReadOnly(permissions.BasePermission):
    def has_object_permission(self, request, view, obj):
        # Read permissions are allowed to any request (GET, HEAD, OPTIONS)
        if request.method in permissions.SAFE_METHODS:
            return True

        # Instance must have an attribute named `owner`.
        return obj.owner == request.user
```

### **38. Fix the N+1 problem using select_related (ForeignKey)**
**Task:** Efficiently fetch all `Books` and their `Author` names in a single query.

#### **Solution:**
```python
# Problem: For N books, it makes 1 query for books + N queries for authors
# Solution: JOIN the tables in the database level
books = Book.objects.select_related('author').all()

for b in books:
    print(b.author.name) # No new query triggered here!

#### **Query Performance Board:**
| Approach | Number of DB Queries |
|---|---|
| Without `select_related` | 1 + N (where N is book count) |
| **With `select_related`** | **1 (Single SQL JOIN)** |
```

---

### **39. Fix the N+1 problem using prefetch_related (M2M)**
**Task:** Efficiently fetch all `Students` and all their related `Courses`.

#### **Solution:**
```python
# prefetch_related does 2 separate queries and joins them in Python
students = Student.objects.prefetch_related('courses').all()

for s in students:
    for c in s.courses.all(): # No new query triggered for courses
        print(c.title)

#### **Query Performance Board:**
| Approach | Number of DB Queries |
|---|---|
| Without `prefetch_related` | 1 + Number of Students |
| **With `prefetch_related`** | **2 (Total)** |
```

---

### **40. Use annotate() to count related objects**
**Task:** For each `Department`, calculate the total number of `Employees`.

#### **Solution:**
```python
from django.db.models import Count

# Logic: Adds a virtual field 'emp_count' to each department object
depts = Department.objects.annotate(emp_count=Count('employees'))

for d in depts:
    print(f"{d.name}: {d.emp_count}")

#### **Result Board:**
| Department | Employee Rows | Resulting `emp_count` |
|---|---|---|
| Engineering | 5 | **5** |
| Sales | 2 | **2** |
```

---

### **41. Use aggregate() for summary calculations**
**Task:** Find the average `price` of all `Products` in the store.

#### **Solution:**
```python
from django.db.models import Avg

# Logic: Returns a dictionary of summary data (not a queryset)
avg_data = Product.objects.aggregate(Avg('price'))
# Result: {'price__avg': 45.50}

#### **Logic Board:**
| Aggregation Type | Returns | Example Result |
|---|---|---|
| `annotate` | QuerySet (Extra fields per row) | `[Dept1(count=5), ...]` |
| **`aggregate`** | **Dictionary (Summary of whole table)** | `{'price__avg': 45.5}` |
```

---

### **42. Filtering APIs using DjangoFilterBackend**
**Task:** Allow users to filter the `Product` list by `category` and `min_price` via URL query params.

#### **Solution:**
```python
# settings.py: INSTALLED_APPS += ['django_filters']

from django_filters.rest_framework import DjangoFilterBackend

class ProductList(generics.ListAPIView):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    filter_backends = [DjangoFilterBackend]
    filterset_fields = ['category', 'price'] # Enabled exact matching
```

---

### **43. Add Search and Ordering to an API**
**Task:** Allow searching by `title` and ordering by `created_at`.

#### **Solution:**
```python
from rest_framework.filters import SearchFilter, OrderingFilter

class PostList(generics.ListAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
    filter_backends = [SearchFilter, OrderingFilter]
    search_fields = ['title', 'content'] # Partial matches allowed
    ordering_fields = ['created_at', 'author']
```

---

### **44. Implement API Throttling (Rate Limiting)**
**Task:** Limit users to 100 requests per day for a specific view.

#### **Solution:**
```python
from rest_framework.throttling import UserRateThrottle

class BurstRateThrottle(UserRateThrottle):
    scope = 'burst' # Defined in settings.py (e.g., '10/min')

class CriticalActionView(APIView):
    throttle_classes = [BurstRateThrottle]

    def post(self, request):
        return Response({"status": "action processed"})
```

---

### **45. View Caching for performance**
**Task:** Cache a heavy report view for 15 minutes.

#### **Solution:**
```python
from django.utils.decorators import method_decorator
from django.views.decorators.cache import cache_page
from django.views.generic import TemplateView

class HeavyReportView(TemplateView):
    template_name = "report.html"

    @method_decorator(cache_page(60 * 15)) # Cache for 15 mins (900 seconds)
    def dispatch(self, *args, **kwargs):
        return super().dispatch(*args, **kwargs)
```

---

### **46. DRF: Custom Validation outside of Serializer**
**Task:** Create a validator function and apply it to a Serializer field.

#### **Solution:**
```python
def validate_no_profanity(value): # Standalone logic
    if "badword" in value.lower():
        raise serializers.ValidationError("Language!")

class ReviewSerializer(serializers.Serializer):
    text = serializers.CharField(validators=[validate_no_profanity])
```

---

### **47. Handle Large Datasets with Pagination**
**Task:** Implement PageNumber pagination (10 per page) globally.

#### **Solution:**
```python
# settings.py
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
```

---

### **48. Testing a DRF Endpoint (APITestCase)**
**Task:** Verify that creating a user returns a 201 status and JSON data.

#### **Solution:**
```python
from rest_framework.test import APITestCase
from django.urls import reverse

class AuthTests(APITestCase):
    def test_registration(self):
        url = reverse('register')
        data = {'username': 'testuser', 'password': 'password123'}
        response = self.client.post(url, data, format='json')
        self.assertEqual(response.status_code, 201)
```

---

### **49. Async View in Django (3.1+)**
**Task:** Create a view that calls an external API asynchronously.

#### **Solution:**
```python
import httpx
from django.http import JsonResponse

async def async_api_call(request):
    async with httpx.AsyncClient() as client:
        r = await client.get('https://api.example.com/data') # Non-blocking I/O
    return JsonResponse(r.json())
```

---

### **50. Use EXPLAIN to analyze a QuerySet**
**Task:** See the database execution plan for a slow query.

#### **Solution:**
```python
# In shell or view
print(Product.objects.filter(price__gt=1000).explain())

# Output: Shows Seq Scan vs Index Scan, Join type, and Cost.
```


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
