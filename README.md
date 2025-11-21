# claude-code

Create a [Framework](http://observablehq.com/framework) app...

```
npx @observablehq/framework@latest create
```

Then

```
cd hello-framework
claude
> /init
```

* https://www.anthropic.com/engineering/claude-code-best-practices

## Claude code install

* Anthropic did not create claude code for integration with an IDE -- (see final Q&A in video)
   * See: [Mastering Claude Code in 30 minutes](https://www.youtube.com/watch?v=6eBSHbLKuN0)
* Don't `npm install -g @anthropic-ai/claude-code`
* Do `curl -fsSL https://claude.ai/install.sh | bash`

## Node.js install

* Using fnm eliminates security concerns by avoiding the need for sudo during installations, 
  preventing third-party libraries from potentially gaining root-level access to your machine 
* https://nodejs.org/en/download
* NVM (Node Version Manager) - Recommended for managing multiple Node.js versions
  * Apparently (not verified): For Apple Silicon Macs (M1/M2/M3), NVM is particularly recommended because it 
  handles ARM architecture compatibility better and allows you to manage different Node.js versions easily.
  The Node.js project itself recommends NVM on their download page, with instructions to install it via curl 
  and then use commands like nvm install 22 to get the latest version.
  If you're looking for what Apple specifically says, they don't have published guidelines on this—Node.js 
  installation is handled by the Node.js community rather than Apple.
* My install -- 19 Nov 2025...
```
# Download and install nvm:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# in lieu of restarting the shell
\. "$HOME/.nvm/nvm.sh"

# Download and install Node.js:
nvm install 24

# Verify the Node.js version:
node -v # Should print "v24.11.1".

# Verify npm version:
npm -v # Should print "11.6.2".

```

## remove defaults

* [Transitioning from Anaconda's `defaults` channels](https://conda-forge.org/docs/user/transitioning_from_defaults/)

## miniforge

* Download the conda-forge installer -- https://conda-forge.org/download/
  * Install as directed (I used `bash Miniforge3-$(uname)-$(uname -m).sh`
* "Miniforge is the preferred conda-forge installer and includes conda, mamba, and their dependencies."
* https://conda-forge.org/docs/user/transitioning_from_defaults/
