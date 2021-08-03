# search and filter in Django 

برای قرار دادن قسمت سرچ و مرتب سازی مراحل زیر را انجام میدهیم : 

1. اضافه کردن ```django_filters``` در نرم افزار های نصب شده در settings.py

2. ساختن فایل serializers.py و ساختن یک کلاس داخل آن که از ModelSerializer ارث بری کند 

   * ساخت کلاس داخلی meta و مشخص کردن model و  fields برای آن

   * ```
     class ArticleSerializer(serializers.ModelSerializer):
         class Meta:
             model = Article
             fields = '__all__'
     ```

3. ساخت کلاسی داخل views که از ListCreateAPIView ارث بری کند

   * مشخص کردن queryset و serializer_class

   * ```
     class ArticlesAPIView(ListCreateAPIView):
         queryset = Article.objects.all()
         serializer_class = ArticleSerializer
     ```

4. اضافه کردن لیستی از search_fields ها به عنوان مواردی که در انها جستجو شود .

   * ```
     search_fields = ['title', 'summery']
     ```

5. اضافه کردن لیستی از filterset_fields ها که در قسمت filter داخل سایت برای انها جایی برای جستجو ایجاد میشود .

   * ```
     filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]
     ```

6. اضافه کردن کد زیر که مشخص میکند چه مواردی در قسمت filter نمایش داده شود :

```filter_backends = [DjangoFilterBackend, SearchFilter, OrderingFilter]```



## Views

### 	Detail View :

​		با استفاده از یک url و pk و مشخص کردن model و template_name یک object را از دیتابیس دریافت کرده و 		هم میتوان از اطلاعات استفاده کرد و هم میتوان تغییر در اطلاعات داد و اینکه object به صورت خودکار                 		داخل template ای که اسم و ادرس ان را در template_name اوردیم قابل استفاده خواهد بود . 

```
class BookDetailView(generic.DetailView):
    model = models.Books
    template_name = 'book_detail.html'
```

### 	List View :

​			با استفاده از یک url وارد کلاس هایی میشویم که از listview ارث بری میکنند و در قسمت model مشخص 			میکنیم کدام class از models ها را نیاز داریم و سپس در قسمت template_name محل html مورد نظر را 			وارد میکنیم و لیستی از object ها را از دیتابیس خواهیم داشت که میتوان انها را تغییر نیز داد 

```
class MyBookBorrowed(LoginRequiredMixin, generic.ListView):
    model = models.BookCopy
    template_name = 'mybook.html'
```

	### create View :

​			اگر بخواهیم از یکی از object های داخل دیتابیس در خود سایت و نه در پنل جنگو بسازیم ، نیازمند کلاسهایی 			هستیم که از createview ارث بری کنند داخل این کلاس ها fields را تعریف میکنیم که در ان مشخص 			میکنیم امکان وارد کردن چه اطلاعاتی باشد و model را هم برای مشخص شدن اینکه از کدام object میخواهیم 			نمونه بسازیم تعریف میکنیم .

```
class BookCreateView(CreateView):
    model = models.Books
    fields = '__all__'
```

​		

	### Update View : 

​			اگر بخواهیم یکی از object های داخل دیتابیس در خود سایت و نه در پنل جنگو تغییر بدهیم  ، نیازمند 			کلاسهایی هستیم که از updateview ارث بری کنند داخل این کلاس ها fields را تعریف میکنیم که در ان 			مشخص میکنیم امکان تغییر دادن چه اطلاعاتی باشد و model را هم برای مشخص شدن اینکه کدام نوع 			object میخواهیم تغییر دهیم تعریف میکنیم .

```
class BookUpdateView(UpdateView):
    model = models.Books
    fields = '__all__'
```

	### Delete View : 

​			اگر بخواهیم یکی از object های داخل دیتابیس در خود سایت و نه در پنل جنگو حذف کنیم  ، نیازمندکلاسهایی 			هستیم که از deleteview ارث بری کنند داخل این کلاس ها fields را تعریف میکنیم که در ان مشخص 			میکنیم امکان حذف کردن چه اطلاعاتی باشد و model را هم برای مشخص شدن اینکه کدام نوع object 			میخواهیم حذف کنیم تعریف میکنیم . سپس success_url را برای اینکه مشخص کنیم در کدام قسمت بعد از 			حذف برویم تعریف میکنیم . 

```
class BookDeleteView(DeleteView):
    model = models.Books
    fields = '__all__'
    success_url = reverse_lazy('All_Book')
```

