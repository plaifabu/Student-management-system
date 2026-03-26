# Student-management-system (Project)
Student Management System using Python with add, update, search, delete, and file storage features
# โครงสร้าง (Data structure)
Import
```python
import json
import os

DATA_FILE = "students.json"
students = []
students = []
```
กันข้อมูลซ้ำ
```python
def is_duplicate(new_student):
    for s in students:
        if s["name"] == new_student["name"] and s["surname"] == new_student["surname"]:
            return True
    return False
```
Load data
```python
def load_from_file():
    global students
    try:
        with open("students.json", "r") as f:
            students = json.load(f)
        print("Loaded data!")
    except:
        print("No file found, start with empty data")
```

Save to File
```python
def save_to_file():
    with open("students.json", "w") as f:
        json.dump(students, f)
    print("Saved!")
```
# ทำเมนูโปรแกรม (Menu)
Create Menu
```python
def menu():
    print("\n===== Student Management =====")
    print("1. Add")
    print("2. Search")
    print("3. Delete")
    print("4. Show All")
    print("5. Exit")
```
ฟังก์ชันเพิ่มข้อมูล (Add)
```python
def add_student():
    student = {}
    student["sex"] = input("Sex: ")
    student["name"] = input("Name: ")
    student["surname"] = input("Surname: ")
    student["birthplace"] = input("Place of Birth: ")
    student["phone"] = input("Phone: ")
    student["emergency_name"] = input("Emergency Name: ")
    student["emergency_phone"] = input("Emergency Phone: ")
    student["pets"] = input("Pets: ")

    if not is_duplicate(student):
        students.append(student)
        print("Added!")
    else:
        print("This student already exists!")
```
ฟังชันก์แก้ไขข้อมูล (Update)
```python
def update_student():
    name = input("Enter name to edit: ")
    found = False

    for s in students:
        if s["name"] == name:
            print("\nUpdate student:", s["name"], s["surname"])

            new_sex = input(f"Sex ({s['sex']}): ")
            new_name = input(f"Name ({s['name']}): ")
            new_surname = input(f"Surname ({s['surname']}): ")
            new_birthplace = input(f"Birthplace ({s['birthplace']}): ")
            new_phone = input(f"Phone ({s['phone']}): ")
            new_emergency_name = input(f"Emergency Name ({s['emergency_name']}): ")
            new_emergency_phone = input(f"Emergency Phone ({s['emergency_phone']}): ")
            new_pets = input(f"Pets ({s['pets']}): ")

            if new_sex:
                s["sex"] = new_sex
            if new_name:
                s["name"] = new_name
            if new_surname:
                s["surname"] = new_surname
            if new_birthplace:
                s["birthplace"] = new_birthplace
            if new_phone:
                s["phone"] = new_phone
            if new_emergency_name:
                s["emergency_name"] = new_emergency_name
            if new_emergency_phone:
                s["emergency_phone"] = new_emergency_phone
            if new_pets:
                s["pets"] = new_pets

            print("Updated!")
            found = True
            break

    if not found:
        print("Not found")
```
ฟังก์ชันค้นหา (Search)
```python
def search_student():
    keyword = input("Search: ")
    found = False

    for s in students:
        if (keyword.lower() in s["name"].lower() or
            keyword.lower() in s["surname"].lower() or
            keyword.lower() in s["sex"].lower()):

            print(f"\n{s['name']} {s['surname']} ({s['sex']})")
            found = True

    if not found:
        print("Not found")
```
ฟังก์ชันลบ (Delete)
```python
def delete_student():
    name = input("Enter name to delete: ")

    for s in students:
        if s["name"] == name:
            students.remove(s)
            print("Deleted!")
            return

    print("Not found")
```
ดูข้อมูลทั้งหมด Show all
```python
def show_all():
    if len(students) == 0:
        print("No data")
        return

    for i, s in enumerate(students, 1):
        print(f"\nStudent {i}")
        print(f"Name: {s['name']}")
        print(f"surname: {s['surname']}")
        print(f"Sex: {s['sex']}")
        print(f"Birthplace: {s['birthplace']}")
        print(f"Phone: {s['phone']}")
        print(f"Emergency: {s['emergency_name']}")
        print(f"emergency_phone: {s['emergency_phone']}")
        print(f"Pets: {s['pets']}")
```
# รันโปรแกรม (Program)
```python
load_from_file()

while True:
    menu()
    choice = input("Choose (1-5): ")

    if choice == "1":
        add_student()
    elif choice == "2":
        update_student()
    elif choice == "3":
        search_student()
    elif choice == "4":
        delete_student()
    elif choice == "5":
        show_all()
    elif choice == "6":
        save_to_file()
        break
    else:
        print("Invalid choice")
```
