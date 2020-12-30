# skeleton

The `skeleton` command created a mirror of the directory structure of a game server. This allows you to create a skeleton directory of custom files, configs, maps etc.

## Commands

Standard: `./gameserver skeleton`

Short: `./gameserver sk`

### Skeleton Directory

The skeleton directory is created in `skel`.

```text
/home/gameserver/skel
```

### Use Case

Skeleton can be used alongside version control software like [git](https://guides.github.com/introduction/git-handbook/) or backed up to save custom configurations for a game server. If a change is added to your git repository/backup it is possible to pull/copy the updates to your game server. If you want to re-deploy a game server you can create a fresh installation and pull/copy in the custom changes over the top of the fresh install.



