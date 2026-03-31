# 6. Write a Program to check if a given graph is a complete graph. Represent the graph using the Adjacency Matrix representation.

#include <iostream>
using namespace std;

int main() {
    int n;

    cout << "Enter number of vertices: ";
    cin >> n;

    int graph[20][20];

    cout << "Enter adjacency matrix:\n";
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> graph[i][j];
        }
    }

    bool isComplete = true;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            if (i == j && graph[i][j] != 0) {
                isComplete = false;
            }

            if (i != j && graph[i][j] != 1) {
                isComplete = false;
            }
        }
    }

    if (isComplete)
        cout << "Graph is a Complete Graph\n";
    else
        cout << "Graph is NOT a Complete Graph\n";

    return 0;
}

<img width="597" height="441" alt="image" src="https://github.com/user-attachments/assets/6cbbfeb7-9db4-4fc4-912a-7b0c21711ae8" />
<img width="596" height="475" alt="image" src="https://github.com/user-attachments/assets/8cb742b9-76bc-4632-b5da-7cfc816764b7" />


# 7. Write a program to check if a given graph is complete graph . Represent the graph using the Adjacency List representation . 

#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n;

    cout << "Enter number of vertices: ";
    cin >> n;

    vector<int> adj[20];
    int edges, u, v;

    cout << "Enter number of edges: ";
    cin >> edges;

    cout << "Enter edges (u v):\n";
    for (int i = 0; i < edges; i++) {
        cin >> u >> v;

        // Undirected graph
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    bool isComplete = true;

    for (int i = 0; i < n; i++) {
        if (adj[i].size() != n - 1) {
            isComplete = false;
            break;
        }
    }

    if (isComplete)
        cout << "Graph is a Complete Graph\n";
    else
        cout << "Graph is NOT a Complete Graph\n";

    return 0;
}

<img width="605" height="484" alt="image" src="https://github.com/user-attachments/assets/0ab857e0-e873-4d44-a094-4d761e3438b9" />
<img width="638" height="448" alt="image" src="https://github.com/user-attachments/assets/f5cc9762-a5c6-46db-9480-ab87c902a418" />


# 8. Write a Program to accept a directed graph G and compute the in-degree and outdegree of each vertex.

#include <iostream>
using namespace std;

int main() {
    int n;

    cout << "Enter number of vertices: ";
    cin >> n;

    int graph[20][20];

    cout << "Enter adjacency matrix:\n";
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cin >> graph[i][j];
        }
    }

    cout << "\nVertex\tIn-Degree\tOut-Degree\n";

    for (int i = 0; i < n; i++) {
        int inDegree = 0, outDegree = 0;

        for (int j = 0; j < n; j++) {
            outDegree += graph[i][j]; // row sum
            inDegree += graph[j][i];  // column sum
        }

        cout << i << "\t" << inDegree << "\t\t" << outDegree << endl;
    }

    return 0;
}

<img width="655" height="476" alt="image" src="https://github.com/user-attachments/assets/3f34e741-7f81-4430-b13d-2719afefd278" />
