# sql_easy

برای ایجاد یک پایگاه داده SQLite و ارتباط با آن در Google Colab آورده شده است. برای اجرا، مراحل زیر را دنبال کنید:
ایجاد یک نوت‌بوک جدید در Google Colab.
کد زیر را در یک سلول جدید درج کرده و سلول را اجرا کنید.
# نصب کتابخانه SQLite
!pip install db-sqlite3
# وارد کردن کتابخانه‌های مورد نیاز
import sqlite3
# ایجاد یک اتصال به پایگاه داده SQLite
conn = sqlite3.connect('sample.db')

# ایجاد یک جدول ساده
conn.execute('''
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY,
        name TEXT NOT NULL,
        age INTEGER NOT NULL
    )
''')
# افزودن داده به جدول
conn.execute("INSERT INTO students (name, age) VALUES (?, ?)", ('John Doe', 25))
conn.execute("INSERT INTO students (name, age) VALUES (?, ?)", ('Jane Doe', 22))
# نمایش اطلاعات
cursor = conn.execute("SELECT * FROM students")
for row in cursor:
    print(row)

# بستن اتصال
conn.close()
این کد یک پایگاه داده ساده با یک جدول به نام "students" ایجاد می‌کند و دو رکورد اضافه می‌کند. نتایج نیز نمایش داده می‌شوند.
به‌منظور دسترسی به پایگاه داده SQLite که در کد بالا ایجاد شده است، می‌توانید از کتابخانه SQLite در زبان Python استفاده کنید. در اینجا نحوه اتصال به پایگاه داده، انجام عملیات CRUD (ساخت، خواندن، به‌روزرسانی و حذف) و نمایش اطلاعات آورده شده است:
# اتصال به پایگاه داده
conn = sqlite3.connect('sample.db')
# ایجاد یک کرسور (cursor) برای اجرای دستورات SQL
cursor = conn.cursor()
# نمایش تمامی ردیف‌ها در جدول
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)
# اضافه کردن یک رکورد جدید
new_student = ('Bob', 23)
cursor.execute("INSERT INTO students (name, age) VALUES (?, ?)", new_student)
conn.commit()
# نمایش تمامی ردیف‌ها پس از اضافه کردن رکورد جدید
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)

# به‌روزرسانی یک رکورد
update_data = ('John Smith', 26, 1)  # نام جدید، سن جدید، شناسه رکورد مورد نظر
cursor.execute("UPDATE students SET name=?, age=? WHERE id=?", update_data)
conn.commit()
# نمایش تمامی ردیف‌ها پس از به‌روزرسانی
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)
# حذف یک رکورد
record_to_delete = (2,)  # شناسه رکورد مورد نظر
cursor.execute("DELETE FROM students WHERE id=?", record_to_delete)
conn.commit()
# نمایش تمامی ردیف‌ها پس از حذف
cursor.execute("SELECT * FROM students")
rows = cursor.fetchall()
for row in rows:
    print(row)
# بستن اتصال
conn.close()
این کد نشان می‌دهد چگونه از کرسور برای اجرای دستورات SQL استفاده کرده و عملیات CRUD را روی جدول "students" انجام داده است. لازم به ذکر است که ممکن است شناسه‌ها و داده‌ها در مثال‌ها با شناسه‌ها و داده‌های موجود در پایگاه داده شما تفاوت داشته باشد، لطفاً آنها را با دقت اصلاح کنید
