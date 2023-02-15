
### مفهوم Middlewere في Express

تعتبر middleware في Express بشكل مبسط دوال لها صلاحية للوصول إلى request و response وتستطيع عمل تغييرات كتنفيذ العمليات أو إنهائها… وغيرها، إذا ألقينا نظرة على المثال التالي سنرى أن جميع الأوامر البرمجية بالمنتصف تعتبر middleware لأنها تقوم بعمليات قبل الرد على الطلب. 

المثال:

    app.get('/users',
            (req,res)=>{
                console.log('users page executed!');
                console.log('this code is a middleware');
                res.send('hello users');}
                );

المخرجات:

    users page executed!
    this code is a middleware

معلومة أخرى، في تعريف الدالة get كالشكل التالي:

    app.get(path, callback [, callback ...])

نلاحظ أنها تستقبل أكثر من دالة لذلك سنقوم بكتابة دالة أخرى كالتالي.

المثال:

    app.get('/users',
            (req,res)=>{
                console.log('users page executed!');
                console.log('this code is a middleware')
                res.send('hello users');},
                (req,res)=> console.log('another function')
                );

المخرجات:

    users page executed!
    this code is a middleware

ما نلاحظه هنا أنه بالرغم من وجود دالة أخرى إلا أنها لم تتنفذ، والسبب هو لأننا لم نقم باستخدام الدالة next. بحيث تزودنا هذهِ الدالة بخاصية الانتقال من دالة middleware إلى أخرى كالتالي. 

المثال:

    app.get('/users',
            (req,res,next)=>{
                console.log('users page executed!');
                console.log('this code is a middleware');
                res.send('hello users');
                next();
            },
                (req,res)=> console.log('another function');
                );


المخرجات:

    users page executed!
    this code is a middleware
    another function



> ملاحظة:  يوجد أنواع لتصنيف middleware ستجدها في Express Documentation.


المصادر:
https://expressjs.com
