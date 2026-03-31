# 1. 
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class SET {
    vector<int> s;

public:
    void input() {
        int n, x;
        cout << "Enter number of elements: ";
        cin >> n;
        s.clear();
        cout << "Enter elements:\n";
        for (int i = 0; i < n; i++) {
            cin >> x;
            if (find(s.begin(), s.end(), x) == s.end())
                s.push_back(x);
        }
    }

    void display() {
        for (int x : s) cout << x << " ";
        cout << endl;
    }

    bool isMember(int x) {
        return find(s.begin(), s.end(), x) != s.end();
    }

    void powerSet() {
        int n = s.size();
        int power = 1 << n;

        for (int i = 0; i < power; i++) {
            cout << "{ ";
            for (int j = 0; j < n; j++) {
                if (i & (1 << j))
                    cout << s[j] << " ";
            }
            cout << "}\n";
        }
    }

    bool isSubset(SET &b) {
        for (int x : s) {
            if (!b.isMember(x))
                return false;
        }
        return true;
    }

    SET unionSet(SET &b) {
        SET result = *this;
        for (int x : b.s) {
            if (!result.isMember(x))
                result.s.push_back(x);
        }
        return result;
    }

    SET intersection(SET &b) {
        SET result;
        for (int x : s) {
            if (b.isMember(x))
                result.s.push_back(x);
        }
        return result;
    }

    SET difference(SET &b) {
        SET result;
        for (int x : s) {
            if (!b.isMember(x))
                result.s.push_back(x);
        }
        return result;
    }

    SET symmetricDifference(SET &b) {
        SET a_b = difference(b);
        SET b_a = b.difference(*this);
        return a_b.unionSet(b_a);
    }

    void cartesianProduct(SET &b) {
        for (int x : s) {
            for (int y : b.s) {
                cout << "(" << x << "," << y << ") ";
            }
        }
        cout << endl;
    }
};

int main() {
    SET A, B, C;
    int choice, x;

    cout << "Enter Set A:\n";
    A.input();

    cout << "Enter Set B:\n";
    B.input();

    do {
        cout << "\nMENU:\n";
        cout << "1. Check Membership\n";
        cout << "2. Power Set\n";
        cout << "3. Subset\n";
        cout << "4. Union\n";
        cout << "5. Intersection\n";
        cout << "6. Difference\n";
        cout << "7. Symmetric Difference\n";
        cout << "8. Cartesian Product\n";
        cout << "0. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter element: ";
            cin >> x;
            cout << (A.isMember(x) ? "Present\n" : "Not Present\n");
            break;

        case 2:
            A.powerSet();
            break;

        case 3:
            cout << (A.isSubset(B) ? "A is subset of B\n" : "Not a subset\n");
            break;

        case 4:
            C = A.unionSet(B);
            C.display();
            break;

        case 5:
            C = A.intersection(B);
            C.display();
            break;

        case 6:
            C = A.difference(B);
            C.display();
            break;

        case 7:
            C = A.symmetricDifference(B);
            C.display();
            break;

        case 8:
            A.cartesianProduct(B);
            break;
        }
    } while (choice != 0);

    return 0;
}

<img width="752" height="788" alt="image" src="https://github.com/user-attachments/assets/4c38622f-2096-4635-95e8-f78011e30aeb" />


