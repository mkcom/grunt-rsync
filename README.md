## grunt-rsync

A Grunt task for accessing the file copying and syncing capabilities of the rsync command line utility. Uses the [rsyncwrapper](https://github.com/jedrichards/rsyncwrapper) npm module for the core functionality.

### Prerequisites

A reasonably modern version of rsync (>=2.6.9) in your PATH.

### Installation

    $ npm install grunt-rsync

### Usage

Add a `rsync` object to your Grunt config. All options defined in the config are past verbatim into [rsyncwrapper](https://github.com/jedrichards/rsyncwrapper), so check that project's readme for more details on the possible options.

For example, the following task config defines three targets. The `dist` target could be used to create a distribution of a website ready for deployment, excluding files related to Git and uncompiled SCSS. The `deploy-staging` and `deploy-live` targets could be used to copy the distribution to the relevant remote hosts over ssh.

```javascript
rsync: {
    dist: {
        src: "./",
        dest: "../dist",
        recursive: true,
        exclude: [".git*","*.scss"]
    },
    deploy-staging: {
        src: "../dist/",
        dest: "/var/www/site-staging",
        host: "user@staging-host",
        recursive: true,
        syncDest: true
    },
    deploy-live: {
        src: "../dist/",
        dest: "/var/www/site",
        host: "user@live-host",
        recursive: true,
        syncDest: true
    }
}
```

### Wildcards, excluding and globbing

Any wildcards, pattern matching and globbing of paths and exclude patterns are handled by rsync itself. So this task does not use Grunt's in-built path expanding and globbing at all. For more information on rsync's sytax check the [rsync manpages](http://linux.die.net/man/1/rsync).