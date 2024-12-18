# insta-cred
A self service tool which creates ephemeral credential that can be checked-out and checked-in by developers in an enterprise SaaS environment 

# Intro
Implementing a check-in/check-out credential system in C involves creating a system that can manage user requests for temporary access to the necessary AWS resources in order to complete pending work. The ability to generate temporary credentials, track its usage, and ensure they are checked in and expired correctly will be covered in the scope of this project. 

C would normally not be the first choice for such a solution, however, we can break the the requirements down into logical modules for credential generation, expiration management, logging, and user management. The project will invoke common tools and libraries to manage access control, timestamps, and logging.

# Setup Instructions
Bespoke steps will go here. 

# Assumptions
Temporary Credentials: This project will simulate temporary credentials as simple strings (e.g., API keys, tokens).
Expiration: Credentials will expire after a specified time period (auto self-destruct) 
Check-in/Check-out: Users check-out credentials, use them, and then check them back in (for reusable creds, versus single-use-only)
Logging: We'll log all actions to a file for audit purposes.
Users will only be allowed to check out a single credential at a time (for this iteration, additional features to be added in the future) 

Libraries: 
    time.h: - Timestamp and Expiration Management
    stdio.h: - Logging actions to files
    stdlib.h: - Memory Management and String Handling
    string.h: - String Manipulations
    pthread.h: - Optional for concurrent access in case of multiple users (not covered in this example, but good for scalability).

Simplified Design / Key Components:
A. Credential Store: A structure to hold credentials and metadata (e.g., creation time, expiration time).
B. Check-in/Check-out Logic: Functions to check-out and check-in credentials, ensuring proper expiration.
C. Logging: A logging function to track events.
D. Main Loop: A simple command-line interface (CLI) to simulate user interactions.

# Sequence 
The order in which the code will be written is as followed: 
1. Define Structures for Credential Management - Create a struct that holds the credential's information, including a unique ID, the time it was created, and its expiration time.
2. Generate a Temporay Credential
3. Check-Out Credential Logic
4. Check-In Credential Logic
5. Logging Function (to write to txt or separate file)
6. Main Loop / CLI Interfacing to enable users to generate credentials, check them out, and check them in

# Key Componenets
Credential Generation: When a user requests access, we generate a temporary credential with a specified duration (tokenization) 
Check-Out: User can request a credential if it is available AND not expired. The system checks the expiration time before granting access to the user.
Check-In: User must "check-in" credential once they are done with it, such that it can be "checked-out" by someone else
Logging: All activity will be written to action_log.txt to provide an audit trail

# Pending Improvements / Extensions
Enhanced Error Handling for edge cases and more precise fault control
When used in a multi-user environment, use of synchronization mechanisms like pthread_mutex_t to avoid race conditions would be of benefit (e.g., two users checking out the same credential)
Security: Ensure the credential is encrypted/stored properly, while access rights are enforced on specific permissions 

# Conclusion 
This architecture provides a robust, secure, and scalable solution for managing on-demand, temporary access to resources in AWS. 
The system ensures that credentials are issued only for a limited time, and users are required to check in credentials after use. 
The audit trail ensures that all actions are tracked for security and compliance purposes. 
This can be improved to accommodate more complex systems with additional features like role-based access control, multi-tenancy, and distributed credential stores in the future. 
