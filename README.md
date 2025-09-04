## ✅ Phase 2: User Login & Roles  

This phase adds a **basic login system** for users with different roles. It introduces authentication and simple role-based access, laying the foundation for more advanced security.  

### Features  
- User accounts are stored in `users.json`.  
- Two example accounts are included by default:  
  - Officer → `jdoe` / password: `1234`  
  - Supervisor → `srogers` / password: `admin123`  
- Officers and supervisors have separate roles.  
- Prevents empty username/password input.  
- Locks out a user after **3 failed login attempts**.  

### Usage  
Run the script:  
```bash
python phase2_access_system.py
