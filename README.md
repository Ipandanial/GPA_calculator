    #include <iostream>
    #include <vector>
    #include <iomanip>
    #include <string>

    using namespace std;

    // Structure to hold subject details
     struct Subject {
    string name;
    int credits;
    float gradePoint;
    };

    // Function to calculate GPA
    float calculateGPA(const vector<Subject>& subjects, int& totalCredits, float& totalQualityPoints) {
    totalCredits = 0;
    totalQualityPoints = 0.0;

    for (const auto& subject : subjects) {
        totalCredits += subject.credits;
        totalQualityPoints += subject.credits * subject.gradePoint;
    }

    return totalCredits > 0 ? totalQualityPoints / totalCredits : 0.0;
    }

    int main() {
    vector<Subject> subjects;
    char choice;

    cout << "UTeM GPA Calculator\n";
    cout << "====================\n";

    do {
        Subject subject;

        // Input subject details
        cout << "\nEnter subject name: ";
        cin.ignore();
        getline(cin, subject.name);

        cout << "Enter credit hours (1-4): ";
        cin >> subject.credits;
        while (subject.credits < 1 || subject.credits > 4) {
            cout << "Invalid input. Please enter credit hours (1-4): ";
            cin >> subject.credits;
        }

        cout << "Enter grade point (4.0 for A, 3.7 for A-, etc.): ";
        cin >> subject.gradePoint;
        while (subject.gradePoint < 0.0 || subject.gradePoint > 4.0) {
            cout << "Invalid input. Please enter grade point (0.0 - 4.0): ";
            cin >> subject.gradePoint;
        }

        subjects.push_back(subject);

        cout << "Do you want to add another subject? (y/n): ";
        cin >> choice;

    } while (choice == 'y' || choice == 'Y');

    // Calculate GPA
    int totalCredits;
    float totalQualityPoints;
    float gpa = calculateGPA(subjects, totalCredits, totalQualityPoints);

    // Display Results
    cout << "\nGPA Calculation Results\n";
    cout << "========================\n";
    cout << "Total Quality Points: " << fixed << setprecision(2) << totalQualityPoints << endl;
    cout << "Total Credits: " << totalCredits << endl;
    cout << "Your GPA: " << fixed << setprecision(2) << gpa << endl;

    return 0;
    }
