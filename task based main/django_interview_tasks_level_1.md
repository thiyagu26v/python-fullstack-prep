---
> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*

---

# Django Live-Task Mastery - Level 1 (Fundamentals)

This document contains practical, "live-coding" style tasks common in technical interviews for Django developers. Every line of code includes a literal comment explaining its purpose.

---

## **Section 1: Models & ORM (Q1-10)**

### **1. Enforce unique combinations in a Model (Meta Options)**
**Task:** Create a `Booking` model where a user cannot book the same room on the same date twice.

#### **Solution:**
```python
from django.db import models

class Booking(models.Model):
    user = models.ForeignKey('auth.User', on_view=models.CASCADE) # Link to auth user
    room = models.CharField(max_length=100)                      # Basic room identifier
    date = models.DateField()                                     # The booking date

    class Meta:
        unique_together = ('room', 'date')  # Ensures no two rows share both room and date

#### **Visual Data Check:**
| Room | Date | Status |
|---|---|---|
| Room A | 2024-01-01 | Allowed |
| Room B | 2024-01-01 | Allowed |
| **Room A** | **2024-01-01** | **Rejected (Duplicate)** |
```

---

### **2. Add a database check constraint for minimum value**
**Task:** In a `Product` model, ensure the `price` is always greater than 0 at the database level.

#### **Solution:**
```python
from django.db import models
from django.db.models import Q, CheckConstraint

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)

    class Meta:
        constraints = [
            CheckConstraint(
                check=Q(price__gt=0),        # Actual logic: price must be > 0
                name='price_must_be_positive' # Internal DB constraint name
            )
        ]

#### **Visual Data Check:**
| Product | Price | Database Action |
|---|---|---|
| Laptop | 1200.00 | Success |
| Mouse | -5.00 | **IntegrityError** |
```

---

### **3. Query for "OR" logic using Q objects**
**Task:** Find all `Post` objects where the title contains "Django" OR the category is "Python".

#### **Solution:**
```python
from django.db.models import Q
from .models import Post

# Logic: Q object wraps the query; | acts as the OR operator
results = Post.objects.filter(
    Q(title__icontains="Django") | Q(category="Python")
)

#### **Result Board:**
| Post Title | Category | In Results? | Why? |
|---|---|---|---|
| Python Basics | Python | Yes | Category match |
| Django Advanced | SQL | Yes | Title match |
| Java Tips | Java | No | No match |
```

---

### **4. Compare two fields in the same row using F expressions**
**Task:** Find all `Employee` records where `current_salary` is higher than `starting_salary`.

#### **Solution:**
```python
from django.db.models import F
from .models import Employee

# Logic: F() allows referencing field values without loading them into memory
leaders = Employee.objects.filter(current_salary__gt=F('starting_salary'))

#### **Result Board:**
| Employee | Start Salary | Current Salary | In Results? |
|---|---|---|---|
| Alice | 50,000 | 55,000 | **Yes** (Current > Start) |
| Bob | 60,000 | 60,000 | No (Equal) |
```

---

### **5. Create a SlugField that automatically populates**
**Task:** In the Admin, make sure the `slug` field for a `Blog` automatically fills based on the `title`.

#### **Solution:**
```python
# In admin.py
from django.contrib import admin
from .models import Blog

@admin.register(Blog)
class BlogAdmin(admin.ModelAdmin):
    prepopulated_fields = {'slug': ('title',)} # Maps slugs to titles in UI
```

---

## **Section 2: Views & Logic (Q11-20)**

### **6. Convert a Function-Based View (FBV) to a Class-Based View (CBV)**
**Task:** Transform a standard list view into a `ListView`.

#### **Solution:**
```python
# Before (FBV)
def product_list(request):
    products = Product.objects.all()
    return render(request, 'list.html', {'products': products})

# After (CBV)
from django.views.generic import ListView

class ProductListView(ListView):
    model = Product              # Automatically fetches Product.objects.all()
    template_name = 'list.html'   # Target template
    context_object_name = 'products' # Name used in the template
```

---

### **7. Restrict access to a view (Function vs Class)**
**Task:** Allow only logged-in users to access the `Profile` view.

#### **Solution:**
```python
# FBV Approach
from django.contrib.auth.decorators import login_required

@login_required # Decorator protects the view
def profile_view(request):
    return render(request, 'profile.html')

# CBV Approach
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import TemplateView

class ProfileView(LoginRequiredMixin, TemplateView): # Mixin MUST come first
    template_name = 'profile.html'
```

---

### **8. Pass extra context to a Generic View**
**Task:** In a `DetailView`, add the current system time to the template context.

#### **Solution:**
```python
from django.views.generic import DetailView
from datetime import datetime

class ArticleDetail(DetailView):
    model = Article

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs) # Get default context first
        context['now'] = datetime.now()             # Add custom variable
        return context
```

---

### **9. Handle a dynamic URL parameter**
**Task:** Create a view that accepts a `category` string from the URL and filters `Items`.

#### **Solution:**
```python
# urls.py: path('items/<str:category>/', views.item_filter)

def item_filter(request, category): # 'category' is passed from URL match
    items = Item.objects.filter(category=category)
    return render(request, 'items.html', {'items': items})
```

---

### **10. Implement a custom 404 handler**
**Task:** Direct users to a custom page when they enter a non-existent URL.

#### **Solution:**
```python
# views.py
def custom_404(request, exception):
    return render(request, '404.html', status=404)

# urls.py (Global scope)
handler404 = 'myapp.views.custom_404'
```

---

## **Section 3: Forms & Validation (Q11-15)**

### **11. Custom field validation in a Form**
**Task:** Ensure the `email` field in a `ContactForm` only accepts addresses ending in `@company.com`.

#### **Solution:**
```python
from django import forms
from django.core.exceptions import ValidationError

class ContactForm(forms.Form):
    email = forms.EmailField()

    def clean_email(self): # Pattern: clean_<fieldname>
        data = self.cleaned_data['email']
        if "@company.com" not in data:
            raise ValidationError("We only accept corporate emails!")
        return data # Always return the cleaned data
```

---

### **12. Exclude fields from a ModelForm**
**Task:** Create a form for `Task` but hide the `created_at` and `updated_at` fields.

#### **Solution:**
```python
from django import forms
from .models import Task

class TaskForm(forms.ModelForm):
    class Meta:
        model = Task
        exclude = ['created_at', 'updated_at'] # Blacklist approach
```

### **13. Global context using a Context Processor**
**Task:** Make a `SITE_NAME` variable available in every template without passing it in every view.

#### **Solution:**
```python
# context_processors.py
def site_info(request):
    return {
        'SITE_NAME': 'VibeVault Portal' # This dictionary is merged into all contexts
    }

# settings.py
# TEMPLATES = [ { 'OPTIONS': { 'context_processors': [ 'myapp.context_processors.site_info', ... ] } } ]
```

---

### **14. Create a custom Template Filter**
**Task:** Create a filter named `multiply` that takes a value and an argument.

#### **Solution:**
```python
# myapp/templatetags/custom_math.py
from django import template

register = template.Library()

@register.filter
def multiply(value, arg):
    return value * arg # Logic: {{ 5|multiply:10 }} -> 50

# Template: {% load custom_math %}
```

---

### **15. Simple logging Middleware**
**Task:** Log the URL of every incoming request to the console.

#### **Solution:**
```python
class LogRequestMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        print(f"Request Path: {request.path}") # Logic before view
        response = self.get_response(request)  # Pass to view/next middleware
        return response
```

---

## **Section 4: Advanced Core Features (Q16-25)**

### **16. Signal: Create a User Profile on signup**
**Task:** Automatically create a `Profile` row whenever a new `User` is created.

#### **Solution:**
```python
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.contrib.auth.models import User
from .models import Profile

@receiver(post_save, sender=User)
def create_profile(sender, instance, created, **kwargs):
    if created: # Only run on the FIRST save (signup)
        Profile.objects.create(user=instance) # Link profile to new user
```

---

### **17. Atomic Transactions to prevent data corruption**
**Task:** Ensure that if a payment fails, the order status isn't updated.

#### **Solution:**
```python
from django.db import transaction

def process_order(order_id):
    with transaction.atomic(): # If ANY line inside fails, the whole block rolls back
        order = Order.objects.select_for_update().get(id=order_id)
        order.status = 'Paid'
        order.save()
        # Imagine payment logic here that might raise an Exception
```

---

### **18. Custom Manager for "Published" posts**
**Task:** Create a manager so you can use `Post.published.all()` instead of filtering every time.

#### **Solution:**
```python
class PublishedManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().filter(status='published')

class Post(models.Model):
    title = models.CharField(max_length=100)
    status = models.CharField(max_length=20, default='draft')
    
    objects = models.Manager()   # Default manager
    published = PublishedManager() # Custom manager

#### **Manager Logic Board:**
| Queryset | Returns |
|---|---|
| `Post.objects.all()` | Every post in DB (Drafts + Published) |
| `Post.published.all()` | **Only** posts with `status='published'` |
```

---

### **19. Override save() method for custom logic**
**Task:** Automatically generate a random reference code for a `Payment` before saving.

#### **Solution:**
```python
import uuid

class Payment(models.Model):
    ref_code = models.CharField(max_length=50, blank=True)

    def save(self, *args, **kwargs):
        if not self.ref_code:
            self.ref_code = str(uuid.uuid4())[:8] # Assign unique code
        super().save(*args, **kwargs)             # Call the original save logic
```

---

### **20. Admin Customization: List display and Search**
**Task:** In Django Admin, show the `email` and `date_joined` for users and add a search bar.

#### **Solution:**
```python
from django.contrib import admin
from .models import CustomUser

class UserAdmin(admin.ModelAdmin):
    list_display = ('username', 'email', 'is_staff') # Columns in list view
    search_fields = ('username', 'email')           # Search query targets
    list_filter = ('is_active',)                     # Sidebar filters

admin.site.register(CustomUser, UserAdmin)
```

---

### **21. Unit Test for a simple View**
**Task:** Write a test to check if the home page returns a 200 status code.

#### **Solution:**
```python
from django.test import TestCase, Client
from django.urls import reverse

class ViewTests(TestCase):
    def test_homepage_status(self):
        client = Client()
        response = client.get(reverse('home')) # Resolve URL name
        self.assertEqual(response.status_code, 200) # Assert expectation
```

---

### **22. Handle File Uploads in a view**
**Task:** Save an uploaded image from a POST request to a `Document` model.

#### **Solution:**
```python
def upload_file(request):
    if request.method == 'POST' and request.FILES['myfile']:
        myfile = request.FILES['myfile'] # File data is in request.FILES
        Document.objects.create(upload=myfile)
        return redirect('success')
```

---

### **23. Pagination in a Function-Based View**
**Task:** Display only 10 items per page.

#### **Solution:**
```python
from django.core.paginator import Paginator

def item_list(request):
    items = Item.objects.all()
    paginator = Paginator(items, 10) # 10 items per page
    page_num = request.GET.get('page')
    page_obj = paginator.get_page(page_num)
    return render(request, 'list.html', {'page_obj': page_obj})
```

---

### **24. Message Framework for user feedback**
**Task:** Show a "Profile Updated" success message after a form save.

#### **Solution:**
```python
from django.contrib import messages

def update_profile(request):
    # ... after successful save ...
    messages.success(request, "Your profile was updated successfully!")
    return redirect('profile')
```

---

### **25. Redirect with parameters**
**Task:** After saving an object, redirect to its detail page using its `id`.

#### **Solution:**
```python
from django.shortcuts import redirect

def create_item(request):
    new_item = Item.objects.create(name="Task")
    return redirect('item_detail', pk=new_item.id) # Use URL name and PK
```


---

> **✨ Created by Thiyagarajan Varadharajan ✨**  
> *Python Full Stack Developer | Interview Prep Resources*
> 
> *Share this resource on LinkedIn!*

---
