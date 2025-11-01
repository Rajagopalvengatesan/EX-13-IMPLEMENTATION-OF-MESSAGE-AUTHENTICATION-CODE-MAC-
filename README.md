## EX 13 : IMPLEMENTATION OF MESSAGE AUTHENTICATION CODE(MAC)


## AIM:

To implement a Message Authentication Code (MAC) using a shared secret key and a hash function to verify the integrity and authenticity of a message.


## ALGORITHM:

1.	Choose a shared secret key that will be known to both the sender and the receiver.
2.	Define the message that needs to be authenticated.
3.	Concatenate the message and the secret key to form a new string.
4.	Apply a hash function (e.g., simple XOR-based hash or any secure hashing function like SHA) to the concatenated string to generate the MAC.
5.	Send the message along with the generated MAC.
6.	For verification, the receiver uses the same shared key, concatenates it with the received message, and applies the hash function to generate a new MAC.
7.	Compare the generated MAC with the received MAC. If they match, the message is authentic; otherwise, it has been tampered with.


## PROGRAM:
```
#include <stdio.h>
#include <string.h>

#define MAC_SIZE 32

void computeMAC(const char *key, const char *message, char *mac) {
    int key_len = strlen(key);
    int msg_len = strlen(message);
    
    for (int i = 0; i < MAC_SIZE; i++) {
        mac[i] = key[i % key_len] ^ message[i % msg_len];
    }
    mac[MAC_SIZE] = '\0';
}

int main() {
    char key[100], message[100];
    char mac[MAC_SIZE + 1];
    char receivedMAC[MAC_SIZE + 1];

    printf("Enter the secret key: ");
    scanf("%s", key);

    printf("Enter the message: ");
    scanf("%s", message);

    computeMAC(key, message, mac);

    printf("Computed MAC (in hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        printf("%02x", (unsigned char)mac[i]);
    }
    printf("\n");

    printf("Enter the received MAC (as hex): ");
    for (int i = 0; i < MAC_SIZE; i++) {
        scanf("%02hhx", &receivedMAC[i]);
    }

    if (memcmp(mac, receivedMAC, MAC_SIZE) == 0) {
        printf("MAC verification successful. Message is authentic.\n");
    } else {
        printf("MAC verification failed. Message is not authentic.\n");
    }

    return 0;
}

```
## OUTPUT:
<img width="750" height="239" alt="image" src="https://github.com/user-attachments/assets/81ac24b2-2065-4f6a-8356-f55b97eaba0d" />

## RESULT:

The Message Authentication Code (MAC) was implemented successfully, allowing the verification	of	message	integrity	and	authenticity	using	a	shared	secret	key.
