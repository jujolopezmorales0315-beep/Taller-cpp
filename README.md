//=======CODIGO 1=======
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cout << "Ingrese el tamaño del array: ";
    cin >> n;
    int arr[n];
    cout << "Ingrese los elementos: ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    sort(arr, arr + n);
    double mediana;
    if (n % 2 == 0)
        mediana = (arr[n/2 - 1] + arr[n/2]) / 2.0;
    else
        mediana = arr[n/2];

    cout << "La mediana es: " << mediana << endl;
    return 0;
}

//=======CODIGO 2=======
#include <iostream>
#include <algorithm>
using namespace std;

int main() {
    int n, x;
    cout << "Ingrese el tamaño del array: ";
    cin >> n;
    int arr[n];
    cout << "Ingrese los elementos (desordenados): ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    sort(arr, arr+n);

    cout << "Ingrese el valor a buscar: ";
    cin >> x;

    int izq = 0, der = n-1, mid;
    bool encontrado = false;

    while (izq <= der) {
        mid = (izq + der) / 2;
        if (arr[mid] == x) { encontrado = true; break; }
        else if (arr[mid] < x) izq = mid + 1;
        else der = mid - 1;
    }

    if (encontrado) cout << "Elemento encontrado en la posición " << mid << endl;
    else cout << "Elemento no encontrado." << endl;
    return 0;
}

//=======CODIGO 3=======
#include <iostream>
using namespace std;

int main() {
    int filas, cols;
    cout << "Ingrese número de filas: ";
    cin >> filas;
    cout << "Ingrese número de columnas: ";
    cin >> cols;

    int mat[filas][cols], trans[cols][filas];
    cout << "Ingrese la matriz: \n";
    for (int i = 0; i < filas; i++)
        for (int j = 0; j < cols; j++)
            cin >> mat[i][j];

    for (int i = 0; i < filas; i++)
        for (int j = 0; j < cols; j++)
            trans[j][i] = mat[i][j];

    cout << "Matriz transpuesta:\n";
    for (int i = 0; i < cols; i++) {
        for (int j = 0; j < filas; j++)
            cout << trans[i][j] << " ";
        cout << endl;
    }
    return 0;
}

//=======CODIGO 4=======
#include <iostream>
using namespace std;

int main() {
    const int MAX = 5;
    string productos[MAX];
    int stock[MAX];

    cout << "Registro de 5 productos:\n";
    for (int i = 0; i < MAX; i++) {
        cout << "Producto " << i+1 << ": ";
        cin >> productos[i];
        cout << "Cantidad: ";
        cin >> stock[i];
    }

    cout << "\n=== INVENTARIO ===\n";
    for (int i = 0; i < MAX; i++)
        cout << productos[i] << " - " << stock[i] << endl;

    return 0;
}

//=======CODIGO 5=======
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Ingrese el tamaño del array: ";
    cin >> n;
    int arr[n];

    cout << "Ingrese los elementos: ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    for (int i = 0; i < n-1; i++) {
        int minIndex = i;
        for (int j = i+1; j < n; j++)
            if (arr[j] < arr[minIndex]) minIndex = j;
        swap(arr[i], arr[minIndex]);
    }

    cout << "Array ordenado: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    return 0;
}

//=======CODIGO 6=======
#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Ingrese el tamaño del array: ";
    cin >> n;
    int arr[n];

    cout << "Ingrese los elementos: ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    cout << "Duplicados encontrados: ";
    bool hayDuplicados = false;
    for (int i = 0; i < n; i++) {
        for (int j = i+1; j < n; j++) {
            if (arr[i] == arr[j]) {
                cout << arr[i] << " ";
                hayDuplicados = true;
                break;
            }
        }
    }
    if (!hayDuplicados) cout << "Ninguno";
    cout << endl;
    return 0;
}

//=======CODIGO 7=======
#include <iostream>
using namespace std;

char tablero[3][3] = { {'1','2','3'}, {'4','5','6'}, {'7','8','9'} };

void mostrarTablero() {
    cout << "\n";
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << tablero[i][j] << " ";
        }
        cout << endl;
    }
}

bool verificarGanador(char jugador) {
    // Revisar filas
    for (int i = 0; i < 3; i++) {
        int contador = 0;
        for (int j = 0; j < 3; j++) {
            if (tablero[i][j] == jugador) contador++;
        }
        if (contador == 3) return true;
    }

    // Revisar columnas
    for (int j = 0; j < 3; j++) {
        int contador = 0;
        for (int i = 0; i < 3; i++) {
            if (tablero[i][j] == jugador) contador++;
        }
        if (contador == 3) return true;
    }

    // Revisar diagonal principal
    int contadorDiag1 = 0;
    for (int i = 0; i < 3; i++) {
        if (tablero[i][i] == jugador) contadorDiag1++;
    }
    if (contadorDiag1 == 3) return true;

    // Revisar diagonal secundaria
    int contadorDiag2 = 0;
    for (int i = 0; i < 3; i++) {
        if (tablero[i][2-i] == jugador) contadorDiag2++;
    }
    if (contadorDiag2 == 3) return true;

    return false;
}

int main() {
    int jugadas = 0, opcion;
    char jugador = 'X';
    while (jugadas < 9) {
        mostrarTablero();
        cout << "Turno del jugador " << jugador << ". Elija posición: ";
        cin >> opcion;

        int fila = (opcion-1) / 3;
        int col = (opcion-1) % 3;

        if (tablero[fila][col] != 'X' && tablero[fila][col] != 'O') {
            tablero[fila][col] = jugador;
            jugadas++;
            if (verificarGanador(jugador)) {
                mostrarTablero();
                cout << "Jugador " << jugador << " gana" << endl;
                return 0;
            }
            jugador = (jugador == 'X') ? 'O' : 'X';
        } else {
            cout << "Posición ocupada. Intente de nuevo.\n";
        }
    }
    mostrarTablero();
    cout << "Empate.\n";
    return 0;
}
