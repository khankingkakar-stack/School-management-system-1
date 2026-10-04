
# School Management System
# Object-Oriented Programming (Inheritance)


# Part 1: Base Class
class Person:
    def __init__(self, name, age, cnic):
        self.name = name
        self.age = age
        self.cnic = cnic

    def display_info(self):
        print("Name:", self.name)
        print("Age:", self.age)
        print("CNIC:", self.cnic)

    def role(self):
        return "Person"


# Part 2: Child Classes

# Student Class
class Student(Person):
    def __init__(self, name, age, cnic, roll_no, marks):
        super().__init__(name, age, cnic)
        self.roll_no = roll_no
        self.marks = marks

    def average(self):
        if len(self.marks) == 0:
            return 0
        return sum(self.marks) / len(self.marks)

    def grade(self):
        avg = self.average()

        if avg >= 80:
            return "A"
        elif avg >= 70:
            return "B"
        elif avg >= 60:
            return "C"
        else:
            return "F"

    def role(self):
        return "Student"

    def display_info(self):
        super().display_info()
        print("Roll Number:", self.roll_no)
        print("Marks:", self.marks)
        print("Average:", round(self.average(), 2))
        print("Grade:", self.grade())


# Teacher Class
class Teacher(Person):
    def __init__(self, name, age, cnic, subject, salary):
        super().__init__(name, age, cnic)
        self.subject = subject
        self.salary = salary

    def annual_salary(self):
        return self.salary * 12

    def role(self):
        return "Teacher"

    def display_info(self):
        super().display_info()
        print("Subject:", self.subject)
        print("Monthly Salary:", self.salary)
        print("Annual Salary:", self.annual_salary())


# Admin Class
class Admin(Person):
    def __init__(self, name, age, cnic, department, salary):
        super().__init__(name, age, cnic)
        self.department = department
        self.salary = salary

    def annual_salary(self):
        return (self.salary * 12) * 1.10

    def role(self):
        return "Admin"

    def display_info(self):
        super().display_info()
        print("Department:", self.department)
        print("Monthly Salary:", self.salary)
        print("Annual Salary with 10% Bonus:",
              self.annual_salary())


# Part 3: Polymorphism

# Creating objects
s1 = Student("Ali", 18, "12345-1234567-1",
             101, [85, 90, 78])

s2 = Student("Ahmed", 19, "12345-7654321-2",
             102, [72, 75, 80])

t1 = Teacher("Sara", 35, "12345-1111111-1",
             "Mathematics", 60000)

t2 = Teacher("Usman", 40, "12345-2222222-2",
             "English", 55000)

a1 = Admin("Khalid", 45, "12345-3333333-3",
           "Administration", 70000)


# List of all school people
school_people = [s1, s2, t1, t2, a1]

# Display information using polymorphism
print("===== SCHOOL MANAGEMENT SYSTEM =====\n")

for person in school_people:
    print("Role:", person.role())
    person.display_info()
    print("-" * 40)


# Part 4: Reports

student_count = 0
teacher_count = 0
admin_count = 0

highest_student = None
total_annual_salary = 0

for person in school_people:

    if isinstance(person, Student):
        student_count += 1

        if (highest_student is None or
                person.average() > highest_student.average()):
            highest_student = person

    elif isinstance(person, Teacher):
        teacher_count += 1
        total_annual_salary += person.annual_salary()

    elif isinstance(person, Admin):
        admin_count += 1
        total_annual_salary += person.annual_salary()


# Print final reports
print("\n===== SCHOOL REPORT =====")

print("Total Students:", student_count)
print("Total Teachers:", teacher_count)
print("Total Admin Staff:", admin_count)

if highest_student is not None:
    print("Top Student:", highest_student.name)
    print("Highest Average:",
          round(highest_student.average(), 2))

print("Total Annual Staff Salary:",
      round(total_annual_salary, 2))
