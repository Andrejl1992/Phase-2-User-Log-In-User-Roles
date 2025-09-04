```python
import json
import getpass
import os

# -----------------------------
# PHASE 2: User Login & Roles
# -----------------------------
# Features:
# 1. Loads user accounts from users.json
# 2. If users.json does not exist, it creates one with example accounts
# 3. Lets a user log in with username + password
# 4. Prevents empty username or password input
# 5. Shows the user’s role (officer or supervisor) after successful login
# 6. Locks user out after 3 failed login attempts
# -----------------------------

USER_FILE = "users.json"  # File where user accounts will be stored


# -----------------------------
# Load users from users.json
# -----------------------------
def load_users():
    if os.path.exists(USER_FILE):
        with open(USER_FILE, "r") as f:
            return json.load(f)
    else:
        # Create default accounts if file does not exist
        users = {
            "jdoe": {"password": "1234", "role": "officer"},
            "srogers": {"password": "admin123", "role": "supervisor"}
        }
        with open(USER_FILE, "w") as f:
            json.dump(users, f, indent=4)
        return users


# -----------------------------
# User login function
# -----------------------------
def login():
    """User login function with input validation"""
    users = load_users()
    attempts = 0

    while attempts < 3:  # allow up to 3 tries
        username = input("Enter username: ").strip().lower()
        # validate username not empty
        if not username:
            print("Username cannot be empty.")
            attempts += 1
            continue

        password = getpass.getpass("Enter password: ").strip()
        # validate password not empty
        if not password:
            print("Password cannot be empty.")
            attempts += 1
            continue

        # check if username exists and password matches
        if username in users and users[username]["password"] == password:
            role = users[username]["role"]
            print(f"\nAccess Granted: Welcome {username} ({role.upper()})")
            return username, role
        else:
            print("Invalid login. Try again.")
            attempts += 1

    # lock out after 3 failed attempts
    print("Too many failed attempts. Access locked.")
    return None, None


# -----------------------------
# Run script directly
# -----------------------------
if __name__ == "__main__":
    user, role = login()
    if user:
        print(f"You are logged in as {user} with role: {role}")
