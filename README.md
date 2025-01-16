# GPA_calculator
def calculate_gpa():
    print("=================================================")
    print(" Program: GPA CALCULATOR")
    print("=================================================")

    # Dynamic size input
    size = int(input("Enter the number of subjects: "))
    subjects = []
    credits = []
    scores = []
    grades = []
    points = []

    # Input details for each subject
    for i in range(size):
        print(f"\nEnter details for subject {i + 1}:")
        subject = input("Name of Subject: ")
        subjects.append(subject)

        while True:
            credit = int(input("Credit Hours (1-4): "))
            if 1 <= credit <= 4:
                credits.append(credit)
                break
            else:
                print("Invalid credit hours! Enter between 1-4.")

        while True:
            score = float(input("Total Score (0-100): "))
            if 0 <= score <= 100:
                scores.append(score)
                break
            else:
                print("Invalid score! Please enter between 0-100.")

    # Determine grades and points
    for score in scores:
        if score >= 80:
            grades.append("A")
            points.append(4.0)
        elif score >= 75:
            grades.append("A-")
            points.append(3.7)
        elif score >= 70:
            grades.append("B+")
            points.append(3.3)
        elif score >= 65:
            grades.append("B")
            points.append(3.0)
        elif score >= 60:
            grades.append("B-")
            points.append(2.7)
        elif score >= 55:
            grades.append("C+")
            points.append(2.3)
        elif score >= 50:
            grades.append("C")
            points.append(2.0)
        elif score >= 47:
            grades.append("C-")
            points.append(1.7)
        elif score >= 44:
            grades.append("D+")
            points.append(1.3)
        elif score >= 40:
            grades.append("D")
            points.append(1.0)
        else:
            grades.append("E")
            points.append(0.0)

    # GPA Calculation
    total_quality_points = sum([points[i] * credits[i] for i in range(size)])
    total_credits = sum(credits)
    gpa = total_quality_points / total_credits

    # Display Results
    print("\n=========================================================")
    print("INDEX  SUBJECT         CREDIT  SCORE  GRADE  POINT")
    print("=========================================================")
    for i in range(size):
        print(f"{i + 1:<6} {subjects[i]:<15} {credits[i]:<7} {scores[i]:<6} {grades[i]:<6} {points[i]:.2f}")
    print("=========================================================")
    print(f"Your GPA for this semester: {gpa:.2f}")
    print("=========================================================")


# Run the program
if __name__ == "__main__":
    calculate_gpa()
