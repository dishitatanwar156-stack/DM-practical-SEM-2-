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


# 2. 
#include <iostream>
using namespace std;

class RELATION {
    int n;
    int mat[10][10];

public:
    void input() {
        cout << "Enter size of set: ";
        cin >> n;

        cout << "Enter relation matrix:\n";
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                cin >> mat[i][j];
    }

    void display() {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                cout << mat[i][j] << " ";
            cout << endl;
        }
    }

    bool isReflexive() {
        for (int i = 0; i < n; i++) {
            if (mat[i][i] != 1)
                return false;
        }
        return true;
    }

    bool isSymmetric() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (mat[i][j] != mat[j][i])
                    return false;
        return true;
    }

    bool isAntiSymmetric() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                if (i != j && mat[i][j] == 1 && mat[j][i] == 1)
                    return false;
        return true;
    }

    bool isTransitive() {
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                for (int k = 0; k < n; k++)
                    if (mat[i][j] && mat[j][k] && !mat[i][k])
                        return false;
        return true;
    }

    void checkRelation() {
        bool r = isReflexive();
        bool s = isSymmetric();
        bool a = isAntiSymmetric();
        bool t = isTransitive();

        cout << "\nReflexive: " << r;
        cout << "\nSymmetric: " << s;
        cout << "\nAnti-Symmetric: " << a;
        cout << "\nTransitive: " << t;

        if (r && s && t)
            cout << "\nRelation is Equivalence Relation\n";
        else if (r && a && t)
            cout << "\nRelation is Partial Order Relation\n";
        else
            cout << "\nRelation is None\n";
    }
};

int main() {
    RELATION R;

    R.input();
    R.display();
    R.checkRelation();

    return 0;
}

<img width="757" height="607" alt="image" src="https://github.com/user-attachments/assets/49090d5f-a001-4f43-b142-c8bec0c90778" />

# 3. 
#include <iostream>
#include <vector>
using namespace std;

// -------- WITHOUT REPETITION --------
void permuteWithoutRepetition(vector<int> &arr, int l, int r) {
    if (l == r) {
        for (int x : arr)
            cout << x << " ";
        cout << endl;
        return;
    }

    for (int i = l; i <= r; i++) {
        swap(arr[l], arr[i]);
        permuteWithoutRepetition(arr, l + 1, r);
        swap(arr[l], arr[i]); // backtrack
    }
}

// -------- WITH REPETITION --------
void permuteWithRepetition(vector<int> &arr, vector<int> &result, int n, int k) {
    if (k == n) {
        for (int x : result)
            cout << x << " ";
        cout << endl;
        return;
    }

    for (int i = 0; i < arr.size(); i++) {
        result[k] = arr[i];
        permuteWithRepetition(arr, result, n, k + 1);
    }
}

int main() {
    int n;
    cout << "Enter number of digits: ";
    cin >> n;

    vector<int> arr(n);
    cout << "Enter digits:\n";
    for (int i = 0; i < n; i++)
        cin >> arr[i];

    int choice;

    cout << "\n1. Permutations WITHOUT repetition\n";
    cout << "2. Permutations WITH repetition\n";
    cout << "Enter choice: ";
    cin >> choice;

    if (choice == 1) {
        cout << "\nPermutations without repetition:\n";
        permuteWithoutRepetition(arr, 0, n - 1);
    }
    else if (choice == 2) {
        vector<int> result(n);
        cout << "\nPermutations with repetition:\n";
        permuteWithRepetition(arr, result, n, 0);
    }
    else {
        cout << "Invalid choice!";
    }

    return 0;
}

# without repetition
<img width="807" height="587" alt="image" src="https://github.com/user-attachments/assets/10034df2-950e-40ce-b5ee-7c7f0c3991b2" />
# with repetition 
<img width="658" height="792" alt="image" src="https://github.com/user-attachments/assets/c4a6b708-6d50-4418-88fb-0b1ae6f8c7c6" />
<img width="568" height="786" alt="image" src="https://github.com/user-attachments/assets/f8e41148-2d43-466c-b220-5e89564ba16a" />

# 4. For any number n, write a program to list all the solutions of the equation x1 + x2 + x3 + ...+ xn = C, where C is a constant (C<=10) and x1, x2, x3,...,xn are nonnegative integers, using brute force strategy.

#include <iostream>
using namespace std;

int x[20]; // to store values of x1, x2, ..., xn

void findSolutions(int n, int C, int index, int sum) {
    // Base case: if we reached last variable
    if (index == n) {
        if (sum == C) {
            // print solution
            for (int i = 0; i < n; i++) {
                cout << x[i] << " ";
            }
            cout << endl;
        }
        return;
    }

    // Try all possible values from 0 to C
    for (int i = 0; i <= C; i++) {
        if (sum + i <= C) {
            x[index] = i;
            findSolutions(n, C, index + 1, sum + i);
        }
    }
}

int main() {
    int n, C;

    cout << "Enter number of variables (n): ";
    cin >> n;

    cout << "Enter constant (C <= 10): ";
    cin >> C;

    cout << "\nSolutions:\n";
    findSolutions(n, C, 0, 0);

    return 0;
}

<img width="760" height="473" alt="image" src="https://github.com/user-attachments/assets/8172a4cb-1cf5-4f71-a15e-ecf6e0804335" />

# 5. Write a Program to evaluate a polynomial function. (For example store f(x) = 4n2 + 2n + 9 in an array and for a given value of n, say n = 5, compute the value of f(n)).

#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int degree;

    cout << "Enter degree of polynomial: ";
    cin >> degree;

    int coeff[20];

    cout << "Enter coefficients from highest degree to constant:\n";
    for (int i = 0; i <= degree; i++) {
        cin >> coeff[i];
    }

    int n;
    cout << "Enter value of n: ";
    cin >> n;

    int result = 0;

    // Evaluate polynomial
    for (int i = 0; i <= degree; i++) {
        result += coeff[i] * pow(n, degree - i);
    }

    cout << "Value of polynomial = " << result << endl;

    return 0;
}

<img width="719" height="398" alt="image" src="https://github.com/user-attachments/assets/581c06c6-9fd2-4194-8a01-66d392d30166" />

