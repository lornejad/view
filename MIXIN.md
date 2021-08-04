# MIXIN 

​	یک نوع از ارث بری است که اجازه میدهد کلاس ها method های خودشان را با بقیه کلاس ها به اشتراک گذارند .

با این ویژگی قاعدتا کد های تکراری بسیار کم میشود  و نکته مهم در اینجا این است که برای ارث بری باید از mixin ارث بری کند 

### [**`PermissionRequiredMixin`**](https://docs.djangoproject.com/en/dev/topics/auth/default/#the-permissionrequiredmixin-mixin)

یک mixin است که چک میکند آیا user لاگین کرده است یا خیر و اگر لاگین نکرده اجازه دسترسی به ان کلاس را به ان نمیدهد .

### **PermissionsMixin**

اگر این را به یکی از مدل ها اضافه کنیم یک سری فیلد هایی به ان اضافه میکند که عبارت اند از  : 

* **is_superuser** 
* `get_user_permissions`**(***obj=None***)** : 
  * یک سری مجوز هایی که user دارد را برمیگردانند . 
  * اگر obj به ان پاس داده شود مجوز های ان obj خاص را برمیگرداند 
* `get_group_permissions`**(***obj=None***)** :
  * با توجه به گروهی که user در ان قرار دارد مجوز ها را برمیگرداند 
* `get_all_permissions`**(***obj=None***)** : 
  * ترکیب مورد اول و دوم 
* `has_perm`(perm ,obj=None)** :
  * به جای perm میتوان یک مجوز یا لیستی از مجوز ها را به ان داد و با توجه به مجوز های user یک boolean برمیگرداند . 
* `has_module_perms`**(***package_name***)** :
* اگر user کلا مجوزی تو این پکیج داشته باشد true برمیگرداند . 