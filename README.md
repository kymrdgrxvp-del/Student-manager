#include <iostream>
#include <vector>
#include <string>
#include <iomanip>
#include <algorithm>
#include <map>
using namespace std;

struct Student
{
    string Name;
    double score;
};

void AddStudent(vector<Student> &students)
{
    Student s;
    cout << "Nhap ten :";
    getline(cin, s.Name);
    cout << "Nhap diem :";
    cin >> s.score;
    cin.ignore();
    students.push_back(s);
    cout << "=> Da them sinh vien " << endl;
    cout << endl;
}

void showList(const vector<Student> &students)
{
    if (students.empty())
    {
        cout << " Danh sach rong !" <<endl;
        cout << endl;
        return;
    }
    cout << string(8, '=') << "Danh sach sinh vien" << string(8, '=') << endl;
    cout << left << setw(5) << "STT" << setw(25) << "TEN" << "DIEM" << endl;
    cout << string(35, '-') << endl;
    for (int i = 0; i < students.size(); i++)
    {
        cout << left << setw(5) << i + 1 << setw(25) << students[i].Name << students[i].score << endl;
    }
    cout << endl;
}

void findTopStudent(const vector<Student> &students)
{
    if (students.empty())
    {
        cout << "Danh sach rong !\n";
        return;
    }
    Student top = students[0];
    for (auto s : students)
    {
        if (top.score < s.score)
        {
            top = s;
        }
    }
    cout << "Sinh vien co diem cao nhat la:" << top.Name << '(' << top.score << ')' << endl;
    cout << endl;
}

void findStudent(const vector<Student> &students)
{
    if (students.empty())
    {
        cout << "Danh sach rong !\n";
        return;
    }
    string key;
    cout << "Nhap ten can tim:";
    getline(cin, key);
    transform(key.begin(), key.end(), key.begin(), ::tolower);
    bool found = false;
    for (auto s : students)
    {
        string name = s.Name;
        transform(name.begin(), name.end(), name.begin(), ::tolower);
        if (key == name)
        {
            cout << "Tim thay sinh vien " << key << '(' << s.score << ')' << endl;
            found = true;
            cout << endl;
        }
    }
    if (!found)
        cout << "Khong tim thay !" << endl;
        cout << endl;
}

void avgScore(const vector<Student> &students)
{
    if (students.empty())
    {
        cout << "Danh sach rong !" << endl;
        return;
    }
    double sum = 0;
    for (auto s : students)
    {
        sum += s.score;
    }
    cout << "Diem TB:" << sum / students.size() << endl;
    cout << endl;
}

void deleteStudent(vector<Student> &students)
{
    if (students.empty())
    {
        cout << "Danh sach rong !";
        return;
    }
    string key;
    cout << "Nhap sinh vien muon xoa:";
    getline(cin, key);
    bool erase = false;
    for (int i = 0; i < students.size(); i++)
    {
        if (students[i].Name == key)
        {
            students.erase(students.begin() + i);
            cout << "=> Da xoa sinh vien: " << key << endl;
            erase = true;
            break;
        }
    }
    if (!erase)
        cout << "INVALID !\n";
        cout << endl;
}

int main()
{
    vector<Student> students;
    while (true)
    {
        cout << string(6, '=') << " MENU " << string(6, '=') << endl;
        cout << "1. Them sinh vien" << endl;
        cout << "2. Xem danh sach" << endl;
        cout << "3. Tim hoc sinh co diem cao nhat" << endl;
        cout << "4. Tim hoc sinh theo ten" << endl;
        cout << "5. Tinh diem TB cua tat ca sinh vien" << endl;
        cout << "6. Xoa sinh vien khoi danh sach" << endl;
        cout << "0. Thoat MENU" << endl;
        int choice;
        cout << "Nhap lua chon cua ban:";
        cin >> choice;
        cout << endl;
        cin.ignore();
        if (choice == 0)
            break;
        else if (choice == 1)
            AddStudent(students);
        else if (choice == 2)
            showList(students);
        else if (choice == 3)
            findTopStudent(students);
        else if (choice == 4)
            findStudent(students);
        else if (choice == 5)
            avgScore(students);
        else if (choice == 6)
            deleteStudent(students);
        else
            cout << "Khong hop le !";
    }
}
