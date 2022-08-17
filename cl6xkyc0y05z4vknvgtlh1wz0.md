## vscode - version 1.70 - What is 3-way merge editor look like and how to disable it? 😂

## What is 3-way merge editor look like?

When you click on **Source control** button on side menu and _merge changes_ file, you should see 3-way merge editor.

![Screenshot from 2022-08-17 18-50-19.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660737081044/HXC3unEct.png align="left")

![Screenshot from 2022-08-17 18-52-20.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660737158424/60H_aBZjb.png align="left")

As you can see, there are 3 parts on screen:

- Your commit: left side
- Theirs commit: right side
- Conflict fixing result: bottom

You can only edit on **result** part!


![Screenshot from 2022-08-17 19-04-40.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660738174479/IUz_u3LJZ.png align="left")

![Screenshot from 2022-08-17 19-05-02.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660738182770/pbfMS_cQv.png align="left")

After **ctrl + s** to save result:

```sh
# to verify
g diff

g add .

# or merge
g rebase --continue
```

You done it!

## How to disable it?

- use **ctrl + shift + p**
- type "json"
- chose "preferences: Open user settings (JSON)"
- add the setting below:

```json
{
    "git.mergeEditor": false
}
```

Now, you can use old way merge editor:

![Screenshot from 2022-08-17 19-16-35.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1660738605823/TxbXNBOzb.png align="left")

## Reference

- [code.visualstudio - updates - v1_70 - 3way-merge-editor-improvements](https://code.visualstudio.com/updates/v1_70#_3way-merge-editor-improvements)
- [How can I disable 3-way merge editor?](https://github.com/microsoft/vscode/issues/157361)