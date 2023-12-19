# laborator-6


#include <iostream>
#include <cmath>

// Clasa abstractă de bază Number
class Number {
public:
    // Funcție virtuală pură pentru media
    virtual double media() const = 0;
    virtual ~Number() {} // Destructor virtual
};

// Clasa derivată Complex
class Complex : public Number {
private:
    double real;
    double imag;

public:
    Complex(double r, double i) : real(r), imag(i) {}

    // Implementare funcție virtuală media pentru Complex
    double media() const override {
        return (std::abs(real) + std::abs(imag)) / 2.0;
    }
};

// Clasa derivată Vector din 10 elemente
class Vector : public Number {
private:
    double elements[10];

public:
    Vector(const double* arr) {
        for (int i = 0; i < 10; ++i) {
            elements[i] = arr[i];
        }
    }

    // Implementare funcție virtuală media pentru Vector
    double media() const override {
        double sum = 0.0;
        for (int i = 0; i < 10; ++i) {
            sum += elements[i];
        }
        return sum / 10.0;
    }
};

// Clasa derivată Matrix 2 pe 2
class Matrix : public Number {
private:
    double matrix[2][2];

public:
    Matrix(const double mat[2][2]) {
        for (int i = 0; i < 2; ++i) {
            for (int j = 0; j < 2; ++j) {
                matrix[i][j] = mat[i][j];
            }
        }
    }

    // Implementare funcție virtuală media pentru Matrix
    double media() const override {
        return (matrix[0][0] + matrix[0][1] + matrix[1][0] + matrix[1][1]) / 4.0;
    }
};

int main() {
    // Creare obiecte
    Complex complexObj(1.0, 2.0);
    double vectorArr[10] = {1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0};
    Vector vectorObj(vectorArr);
    double matrixArr[2][2] = {{1.0, 2.0}, {3.0, 4.0}};
    Matrix matrixObj(matrixArr);

    // Creare masiv de pointeri la clasa abstractă
    Number* numbers[3];
    numbers[0] = &complexObj;
    numbers[1] = &vectorObj;
    numbers[2] = &matrixObj;

    // Accesarea funcției virtuale media prin pointeri
    for (int i = 0; i < 3; ++i) {
        std::cout << "Media obiectului " << i + 1 << ": " << numbers[i]->media() << std::endl;
    }

    return 0;
}
