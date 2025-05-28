# calender-400-years
developed using c++

code:
#include <iostream>

using namespace std;

// Function to check leap year
bool isLeap(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}

// Get days in a month
int getDaysInMonth(int month, int year) {
    switch (month) {
        case 1: return 31;
        case 2: return isLeap(year) ? 29 : 28;
        case 3: return 31;
        case 4: return 30;
        case 5: return 31;
        case 6: return 30;
        case 7: return 31;
        case 8: return 31;
        case 9: return 30;
        case 10: return 31;
        case 11: return 30;
        case 12: return 31;
        default: return 0;
    }
}

// Get the weekday of the first day of the year (0=Sun, 1=Mon,...)
int getWeekday(int year) {
    int d = 1, m = 1;
    if (m < 3) {
        m += 12;
        year--;
    }
    int k = year % 100;
    int j = year / 100;
    int weekday = (d + 13 * (m + 1) / 5 + k + k / 4 + j / 4 + 5 * j) % 7;
    return (weekday + 6) % 7; // Adjust to make Sunday = 0
}

// Print calendar for a month
void printMonth(int month, int year, int &weekday) {
    string months[] = { "January", "February", "March", "April", "May", "June",
                        "July", "August", "September", "October", "November", "December" };
    int days = getDaysInMonth(month, year);

    cout << "\n  " << months[month - 1] << " " << year << "\n";
    cout << "  Sun  Mon  Tue  Wed  Thu  Fri  Sat\n";

    for (int i = 0; i < weekday; ++i)
        cout << "     ";

    for (int day = 1; day <= days; ++day) {
        cout << setw(5) << day;
        if (++weekday == 7) {
            cout << endl;
            weekday = 0;
        }
    }
    cout << endl;
}

// Print calendar for a year
void printYear(int year) {
    int weekday = getWeekday(year);
    for (int month = 1; month <= 12; ++month)
        printMonth(month, year, weekday);
}

// Print 400 years calendar
void print400Years(int startYear) {
    for (int year = startYear; year < startYear + 400; ++year) {
        printYear(year);
        cout << "\n-----------------------------------\n";
    }
}

int main() {
    int choice, year;
    do {
        cout << "\n====== 400 Years Calendar Menu ======\n";
        cout << "1. Print calendar for a specific year\n";
        cout << "2. Print 400 years calendar from a start year\n";
        cout << "3. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter year: ";
                cin >> year;
                printYear(year);
                break;
            case 2:
                cout << "Enter starting year: ";
                cin >> year;
                print400Years(year);
                break;
            case 3:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice.\n";
        }
    } while (choice != 3);

    return 0;
}
