#include <iostream>
#include <iomanip>
#include <string>
#include <vector>
using namespace std;

struct User {
    string username;
    string password;
};

struct Material {
    string name;
    float price;
};

struct Proforma {
    string clientName;
    vector<pair<string, pair<int, float>>> items; // Material name, quantity, total cost
    float totalCost;
};

vector<User> users;
vector<Material> materials;
vector<Proforma> proformas;

void registerUser() {
    cout << "\n=== Registro de Usuario ===\n";
    User newUser;
    cout << "Ingrese nombre de usuario: ";
    cin >> newUser.username;
    cout << "Ingrese contrasena: ";
    cin >> newUser.password;
    users.push_back(newUser);
    cout << "Usuario registrado con exito!\n";
}

bool loginUser() {
    string username, password;
    cout << "\n=== Inicio de Sesion ===\n";
    cout << "Nombre de usuario: ";
    cin >> username;
    cout << "Contrasena: ";
    cin >> password;

    for (const auto& user : users) {
        if (user.username == username && user.password == password) {
            cout << "\nInicio de sesion exitoso!\n";
            return true;
        }
    }
    cout << "\nUsuario o contrasena incorrectos.\n";
    return false;
}

void addMaterial() {
    cout << "\n=== Ingreso de Material ===\n";
    int materialCount;
    cout << "Cuantos materiales desea ingresar? ";
    cin >> materialCount;

    for (int i = 0; i < materialCount; ++i) {
        Material newMaterial;
        cout << "Nombre del material: ";
        cin >> newMaterial.name;
        cout << "Precio del material: ";
        cin >> newMaterial.price;
        materials.push_back(newMaterial);
    }
    cout << "Materiales ingresados con exito!\n";
}

void createProforma() {
    if (materials.empty()) {
        cout << "\nNo hay materiales disponibles para crear una proforma.\n";
        return;
    }

    Proforma newProforma;
    cout << "\n=== Creacion de Proforma ===\n";
    cout << "Ingrese el nombre del cliente: ";
    cin.ignore();
    getline(cin, newProforma.clientName);

    float totalCost = 0;
    int materialChoice;
    do {
        cout << "\nMateriales disponibles:\n";
        for (size_t i = 0; i < materials.size(); i++) {
            cout << i + 1 << ". " << materials[i].name << " - $" << materials[i].price << "\n";
        }
        cout << materials.size() + 1 << ". Terminar seleccion\n";
        cout << "Seleccione el numero del material: ";
        cin >> materialChoice;

        if (materialChoice > 0 && materialChoice <= materials.size()) {
            int quantity;
            cout << "Ingrese la cantidad: ";
            cin >> quantity;

            float cost = materials[materialChoice - 1].price * quantity;
            newProforma.items.push_back({materials[materialChoice - 1].name, {quantity, cost}});
            totalCost += cost;
        } else if (materialChoice != materials.size() + 1) {
            cout << "Seleccion invalida. Intente de nuevo.\n";
        }
    } while (materialChoice != materials.size() + 1);

    newProforma.totalCost = totalCost;
    proformas.push_back(newProforma);
    cout << "Proforma creada con exito!\n";
}

void viewProformas() {
    if (proformas.empty()) {
        cout << "\nNo hay proformas creadas.\n";
        return;
    }

    cout << "\n=== Lista de Proformas ===\n";
    for (size_t i = 0; i < proformas.size(); ++i) {
        cout << "\nProforma " << i + 1 << "\n";
        cout << "Cliente: " << proformas[i].clientName << "\n";
        cout << "-----------------------------------\n";
        cout << left << setw(15) << "Material" << setw(10) << "Cantidad" << "Costo" << "\n";
        for (const auto& item : proformas[i].items) {
            cout << left << setw(15) << item.first << setw(10) << item.second.first << "$" << item.second.second << "\n";
        }
        cout << "-----------------------------------\n";
        cout << "Total: $" << proformas[i].totalCost << "\n";
    }
}

void deleteProforma() {
    if (proformas.empty()) {
        cout << "\nNo hay proformas para eliminar.\n";
        return;
    }
    int choice;
    cout << "\n=== Eliminacion de Proforma ===\n";
    viewProformas();
    cout << "Seleccione el numero de la proforma a eliminar: ";
    cin >> choice;

    if (choice < 1 || choice > proformas.size()) {
        cout << "Seleccion invalida.\n";
        return;
    }

    proformas.erase(proformas.begin() + (choice - 1));
    cout << "Proforma eliminada con exito!\n";
}

void mainMenu();

void userMenu() {
    int option;
    do {
        cout << "\n=== Menu de Usuario ===\n";
        cout << "1. Creacion de Proformas\n";
        cout << "2. Ver Proformas\n";
        cout << "3. Eliminar Proformas\n";
        cout << "4. Ingreso de Materiales\n";
        cout << "5. Cerrar Sesion\n";
        cout << "Seleccione una opcion: ";
        cin >> option;

        switch (option) {
            case 1:
                createProforma();
                break;
            case 2:
                viewProformas();
                break;
            case 3:
                deleteProforma();
                break;
            case 4:
                addMaterial();
                break;
            case 5:
                cout << "\nCerrando sesion...\n";
                break;
            default:
                cout << "\nOpcion invalida. Intente de nuevo.\n";
        }
    } while (option != 5);
}

void mainMenu() {
    int option;
    do {
        cout << "\n=== Menu Principal ===\n";
        cout << "1. Registrar Usuario\n";
        cout << "2. Iniciar Sesion\n";
        cout << "3. Salir\n";
        cout << "Seleccione una opcion: ";
        cin >> option;

        switch (option) {
            case 1:
                registerUser();
                break;
            case 2:
                if (loginUser()) {
                    userMenu();
                }
                break;
            case 3:
                cout << "\nSaliendo del programa...\n";
                break;
            default:
                cout << "\nOpcion invalida. Intente de nuevo.\n";
        }
    } while (option != 3);
}

int main() {
    mainMenu();
    return 0;
}
