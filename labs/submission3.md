 ## 1. Benefits of Signing Commits for Security
- **Authenticity**: Confirms that the commit was created by the claimed author.  
- **Integrity**: Protects code from tampering by ensuring commits haven’t been altered.  
- **Accountability**: Provides verifiable ownership of changes.  
- **Trust in CI/CD**: Signed commits reduce risk of malicious code entering pipelines.  
- **Compliance**: Helps meet security and audit requirements in regulated environments.  

---

## 2. Evidence of Successful SSH Key Setup and Configuration
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "email@example.com"

# Configure Git for SSH Signing
git config --global user.signingkey <YOUR_SSH_KEY>
git config --global commit.gpgSign true
git config --global gpg.format ssh

# Test connection to GitHub
ssh -T git@github.com
# Expected response:
# Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```
![text](Success.png)

## 3. Why Is Commit Signing Critical in DevSecOps Workflows?

- **Prevents Supply Chain Attacks**: Signed commits stop unauthorized code injection.  
- **Ensures Traceability**: Every change can be linked to a verified contributor.  
- **Strengthens Zero-Trust Model**: No implicit trust; every commit is validated.  
- **Protects Production Environments**: Only signed and verified commits are promoted through CI/CD pipelines.  
- **Supports Security Policies**: Enforces organizational rules for secure collaboration.  

## 4. Screenshots of the "Verified" badge on GitHub

-
