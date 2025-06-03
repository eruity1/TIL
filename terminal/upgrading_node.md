# Upgradging Your Node Version

** I AM USING A macOS Sequoia 15.5 with an on a M1 Mac mini **

1. Checking your node and npm version
```bash
node -v
npm -v
```
(If you need to install node download it here [Node Download](https://nodejs.org/en/download)
I use NVM (Node Version Manager) so I selected NVM)
 * Depending on the version you just installed you don't need to do the following

2. Update NVM (optional)
```bash
nvm install node --reinstall-packages-from=node
```

3. Updgrade Node.js
To get the latest version
```bash
nvm install node
```
To install a certain version
```bash
nvm install <version>
```

4. Switch to that node
If you see `Now using node vXX.XX.X (npm vXX.X.X)` after step 2 you are set
```bash
nvm use node
```
Or if you want a certain version `nvm use <version>`

5. Set that version as the default (Optional)
`nvm alias default node` or `nvm alias default <version>`

6. Check the New Version
```bash
node -v
npm -v
```


