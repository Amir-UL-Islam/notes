### Installation Issue with Permission
Solution: How to fix EACCES errors with NPM on MacOS
```bash
sudo chown -R `whoami` ~/.npm
sudo chown -R `whoami` /usr/local/lib/node_modules
```