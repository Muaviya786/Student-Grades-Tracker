# Student-Grades-Tracker

student_grades = {}


def add_student_grades(name, subject_grades):
    if name in student_grades:
        print(f"Student '{name}' already exists. Updating grades.")
        student_grades[name].update(subject_grades)
    else:
        student_grades[name] = subject_grades
    print(f"Grades for '{name}' added/updated successfully.")

    display_student_report(name)


def calculate_average(grades):
    return sum(grades) / len(grades)


def determine_letter_grade(average):
    if average >= 90:
        return 'A'
    elif average >= 80:
        return 'B'
    elif average >= 70:
        return 'C'
    elif average >= 60:
        return 'D'
    elif average >= 50:
        return 'E'
    else:
        return 'F'


def display_student_report(name):
    if name in student_grades:
        subject_grades = student_grades[name]
        overall_grades = []

        print(f"\nReport for {name}:")
        for subject, grades in subject_grades.items():
            subject_avg = calculate_average(grades)
            overall_grades.extend(grades)  
            letter_grade = determine_letter_grade(subject_avg)
            print(f"{subject}: Grades: {grades}, Grade: {letter_grade}")

        overall_avg = calculate_average(overall_grades)
        overall_letter_grade = determine_letter_grade(overall_avg)
        print(f"Overall Average: {overall_avg:.2f}, Overall Letter Grade: {overall_letter_grade}\n")
    else:
        print(f"Student '{name}' not found.")


def display_all_students():
    if student_grades:
        for name in student_grades:
            display_student_report(name)
    else:
        print("No students found.")


while True:
    print("\n--- Student Grades Management ---")
    print("1. Add student and grades")
    print("2. View all students and grades")
    print("3. Exit")

    choice = input("Enter your choice (1-3): ")

    if choice == '1':
        name = input("Enter the student's name: ")

        subject_grades = {}
        num_subjects = int(input("How many subjects? "))
        for _ in range(num_subjects):
            subject = input("Enter subject name: ")
            subject_grades[subject] = []

            while True:
                grade = input(f"Enter a grade for {subject} (or type 'done' to finish): ")
                if grade.lower() == 'done':
                    break
                try:
                    subject_grades[subject].append(int(grade))
                except ValueError:
                    print("Invalid grade. Please enter a valid number.")

        add_student_grades(name, subject_grades)

    elif choice == '2':
        display_all_students()

    elif choice == '3':
        print("Exiting the program.")
        break

    else:
        print("Invalid choice. Please choose between 1 and 3.")
