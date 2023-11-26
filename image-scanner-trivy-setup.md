
## Deployment

To deploy this project on ubuntu server run

```bash
wget https://github.com/aquasecurity/trivy/releases/download/v0.18.3/trivy_0.18.3_Linux-64bit.deb
sudo dpkg -i trivy_0.18.3_Linux-64bit.deb

```

## Test a sample image (Optional)
```bash
$ trivy image [YOUR_IMAGE_NAME]
$ trivy image python:3.4-alpine

```
## Example:
```bash
$ trivy image python:3.4-alpine
```
