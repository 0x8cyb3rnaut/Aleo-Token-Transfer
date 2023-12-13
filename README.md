# Aleo-Token-Transfer-s         
Aleo Token Transfer is a Python script that enables users to send tokens on the Aleo blockchain to specified recipients. With this script, you can easily initiate secure and private token transfers between Aleo wallets.
import requests

def send_tokens(sender_private_key, recipient_address, amount):
    api_url = "https://api.aleo.org/v1/transactions"
    headers = {"Content-Type": "application/json"}
    payload = {
        "type": "transfer",
        "inputs": [
            {
                "privateKey": sender_private_key,
                "amount": amount
            }
        ],
        "outputs": [
            {
                "address": recipient_address,
                "amount": amount
            }
        ]
    }
    
    response = requests.post(api_url, json=payload, headers=headers)
    
    if response.status_code == 200:
        transaction_data = response.json()
        if "hash" in transaction_data:
            transaction_hash = transaction_data["hash"]
            return transaction_hash
        else:
            return "Error: Transaction failed."
    else:
        return "Error: Transaction failed."

if __name__ == "__main__":
    print("Welcome to Aleo Token Transfer!")
    sender_private_key = input("Enter the sender's private key: ")
    recipient_address = input("Enter the recipient's address: ")
    amount = float(input("Enter the amount of tokens to send: "))
    
    transaction_hash = send_tokens(sender_private_key, recipient_address, amount)
    print(f"Transaction Hash: {transaction_hash}")
