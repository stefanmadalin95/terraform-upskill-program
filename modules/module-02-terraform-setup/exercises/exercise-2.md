# 📝 Exercise 2: Install the AWS CLI

## Objective

Install the AWS CLI to connect to AWS resources.

---

## Steps

✅ Visit the [AWS CLI installation guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).  
✅ For your OS:

- **macOS (with Homebrew)**:

```bash
brew install awscli
```

- **Windows**: Download and run the .msi installer.

- **Linux**:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```


✅ Verify installation:

```bash
aws --version
```

---

➡️ **Next Exercise:** [🧪 Exercise 3: Configure AWS CLI and Credentials](./exercise-3.md)