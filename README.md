# Ex-10-Diffie-Hellman-Key-Exchange-Algorithm

## Aim:
To securely exchange keys between two parties (Alice and Bob) using the Diffie-Hellman key exchange method.

## Algorithm:

1. Public parameters p (prime) and g (primitive root mod p) are known.
2. Each party (Alice and Bob) chooses a secret key.
3. Alice computes her public key: A = g^a mod p.
4. Bob computes his public key: B = g^b mod p.
5. Alice and Bob exchange their public keys.
6. Alice computes the shared secret: S = B^a mod p.
7. Bob computes the shared secret: S = A^b mod p.
8. Both arrive at the same shared secret.

## Program:

```
#include <iostream>
#include <cmath>

using namespace std;

// Function to perform modular exponentiation
// It returns (base^exp) % mod
long long modExp(long long base, long long exp, long long mod) {
    long long result = 1;
    base = base % mod;
    
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1; // exp = exp / 2
        base = (base * base) % mod;
    }
    
    return result;
}

int main() {
    // Publicly known values
    long long p = 23; // A prime number
    long long g = 5;  // A primitive root modulo p

    // Alice's secret key
    long long a = 6; // Chosen privately by Alice
    // Bob's secret key
    long long b = 15; // Chosen privately by Bob

    // Alice calculates A = g^a % p
    long long A = modExp(g, a, p);

    // Bob calculates B = g^b % p
    long long B = modExp(g, b, p);

    // Publicly shared values A and B
    cout << "Publicly shared values: " << endl;
    cout << "A (Alice's public key): " << A << endl;
    cout << "B (Bob's public key): " << B << endl;

    // Alice computes the shared secret S = B^a % p
    long long sharedSecretA = modExp(B, a, p);

    // Bob computes the shared secret S = A^b % p
    long long sharedSecretB = modExp(A, b, p);

    cout << "Shared secret calculated by Alice: " << sharedSecretA << endl;
    cout << "Shared secret calculated by Bob: " << sharedSecretB << endl;

    // Both should have the same shared secret
    if (sharedSecretA == sharedSecretB) {
        cout << "The shared secret is successfully established!" << endl;
    } else {
        cout << "Error: The shared secrets do not match!" << endl;
    }

    return 0;
}
```
## Output:

![image](https://github.com/user-attachments/assets/3078b326-b365-45e6-b00b-16a9bca0f349)

## Result:
The Diffie-Hellman key exchange algorithm is successfully implemented, and both parties arrive at the same shared secret.
