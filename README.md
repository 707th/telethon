استيراد  asyncio
استيراد  difflib
استيراد  shlex
من  كتابة  استيراد  Tuple
استيراد  النظم

# في حالة وجود أي متطلبات ، قم بتثبيت هذا المطلب
async  def  lines_differnce ( file1 ، file2 ):
    مع  فتح ( file1 ) كـ  f1 :
        الخطوط 1  =  f1 . readlines ()
        خطوط 1  = [ سطر . rstrip ( " \ n " ) للخط  في الأسطر  1 ] 
    مع  فتح ( file2 ) كـ  f2 :
        الخطوط 2  =  f2 . readlines ()
        خطوط 2  = [ سطر . rstrip ( " \ n " ) للخط  في الأسطر  2 ] 
    فرق  =  فرق . الفارق الموحد (
        الأسطر 1 ، الأسطر 2 ، fromfile = file1 ، tofile = file2 ، lineterm = " " ، n = 0
    )
    خطوط  =  قائمة ( فرق ) [ 2 :]
    تمت الإضافة  = [ السطر [ 1 :] للخط  في السطور  إذا كان السطر [ 0 ] == " +" ]    
    تمت الإزالة  = [ السطر [ 1 :] للسطر الموجود في  السطر إذا كان السطر [ 0 ] == " - " ]     
    الإضافات  = [ i  for  i  in  added  if  i  not  in  remove ]
    removet  = [ i  for  i  in  إزالتها  إذا  لم أُضيف ] _  _  
    عودة  الإضافات ، إزالتها


غير متزامن  def  runcmd ( cmd : str ) ->  Tuple [ str ، str ، int ، int ]:
    أرجس  =  شلكس . انقسام ( كمد )
    العملية  =  انتظار  asyncio . create_subprocess_exec (
        * args ، stdout = asyncio . عملية فرعية . الأنابيب ، stderr = asyncio . عملية فرعية . يضخ
    )
    stdout ، stderr  =  انتظار  العملية . التواصل ()
    عودة (
        stdout . فك ( "utf-8" ، "استبدال" ). قطاع () ،
        ستدير . فك ( "utf-8" ، "استبدال" ). قطاع () ،
        عملية . رمز الإرجاع
        عملية . pid _
    )


غير متزامن  def  update_requirements ( رئيسي ، اختبار ):
    أ ، ص  =  انتظار  lines_differnce ( رئيسي ، اختبار )
    جرب :
        بالنسبة  لي  في  : _
            انتظار  runcmd ( f "تثبيت النقطة { i } " )
            print ( "تنزيل المكاتب: { i } " )
    باستثناء  الاستثناء  كـ  e :
        print ( f "عذرا هناك خطا في تنزيل المكاتب: { str ( e ) } " )

حلقة  =  asyncio . get_event_loop ()
حلقة . run_until_complete ( update_requirements ( sys . argv [ 1 ]، sys . argv [ 2 ]))
حلقة . إغلاق ()

