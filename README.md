#include <iostream>
#include <vector>
#include <string>

using namespace std;

void torresHanoi(int n, char origen, char auxiliar, char destino) {
    if (n == 1) {
        cout << "Mover disco 1 de " << origen << " a " << destino << endl;
    } else {
        torresHanoi(n - 1, origen, destino, auxiliar);
        cout << "Mover disco " << n << " de " << origen << " a " << destino << endl;
        torresHanoi(n - 1, auxiliar, origen, destino);
    }
}

int busquedaBinaria(vector<int>& arr, int izq, int der, int clave) {
    if (izq > der)
        return -1; 
    
    int medio = izq + (der - izq) / 2;
    
    if (arr[medio] == clave)
        return medio;
    else if (arr[medio] > clave)
        return busquedaBinaria(arr, izq, medio - 1, clave);
    else
        return busquedaBinaria(arr, medio + 1, der, clave);
}


void generarSubconjuntos(string cad, string actual, int indice) {
    if (indice == cad.size()) {
        cout << actual << endl;  
        return;
    }
  
    generarSubconjuntos(cad, actual, indice + 1);
   
    generarSubconjuntos(cad, actual + cad[indice], indice + 1);
}

int main() {
    int opcion;
    do {
        cout << "\nFunciones recursivas avanzadas:\n";
        cout << "1. Torres de Hanoi\n";
        cout << "2. Búsqueda binaria recursiva\n";
        cout << "3. Generar subconjuntos de una cadena\n";
        cout << "4. Salir\n";
        cout << "Elige una opción: ";
        cin >> opcion;

        switch (opcion) {
            case 1: {
                int n;
                cout << "Número de discos: ";
                cin >> n;
                cout << "Movimientos para resolver Torres de Hanoi:\n";
                torresHanoi(n, 'A', 'B', 'C');
                break;
            }
            case 2: {
                int n, clave;
                cout << "Cantidad de elementos ordenados: ";
                cin >> n;
                vector<int> arr(n);
                cout << "Ingresa los elementos ordenados:\n";
                for (int i = 0; i < n; i++) cin >> arr[i];
                cout << "Número a buscar: ";
                cin >> clave;
                int resultado = busquedaBinaria(arr, 0, n - 1, clave);
                if (resultado != -1)
                    cout << "Elemento encontrado en la posición: " << resultado << endl;
                else
                    cout << "Elemento no encontrado.\n";
                break;
            }
            case 3: {
                string cad;
                cout << "Ingresa una cadena: ";
                cin.ignore();
                getline(cin, cad);
                cout << "Subconjuntos generados:\n";
                generarSubconjuntos(cad, "", 0);
                break;
            }
            case 4:
                cout << "Saliendo...\n";
                break;
            default:
                cout << "Opción inválida.\n";
        }
    } while (opcion != 4);

    return 0;
}
