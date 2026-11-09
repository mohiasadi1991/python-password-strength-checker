import string
import getpas

COMMON_PASSWORDS = {
    "password", "12345678", "qwerty123",
    "admin123", "welcome123"
}

def check_password(password):
    score = 0
    feedback = []

    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        feedback.append("Use at least 8 characters.")

    if any(c.islower() for c in password):
        score += 1
    else:
        feedback.append("Add lowercase letters.")

    if any(c.isupper() for c in password):
        score += 1
    else:
        feedback.append("Add uppercase letters.")

    if any(c.isdigit() for c in password):
        score += 1
    else:
        feedback.append("Add numbers.")

    if any(c in string.punctuation for c in password):
        score += 1
    else:
        feedback.append("Add special characters.")

    if password.lower() in COMMON_PASSWORDS:
        score = 0
        feedback.append("Avoid common passwords.")

    if score <= 2:
        strength = "Weak"
    elif score <= 4:
        strength = "Medium"
    else:
        strength = "Strong"

    return strength, feedback

def main():
    print("=== Password Strength Checker ===")

    password = getpass.getpass("Enter password: ")

    strength, feedback = check_password(password)

    print(f"\nPassword strength: {strength}")

    if feedback:
        print("\nSuggestions:")
        for item in feedback:
            print(f"- {item}")
    else:
        print("Great! Your password meets all checks.")

if __name__ == "__main__":
    main()
