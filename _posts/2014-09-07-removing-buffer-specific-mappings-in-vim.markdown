---
  layout: default
---
Removing Buffer-Specific Mappings In Vim
========================================

Until recently, I was mapping `<Leader>`` in insert mode to create the three
pairs of tildes that are used in Github-style markdown to delineate a code
block:

{% gist 99a63b9c0f07d179d977 %}

I expected the mapping to do the following:

    ```
    // Code block here.
    ```

Later on, I realized that it was not a good idea, because it overshadows my
shortcut for putting only one pair of tildes after pressing the space bar,
where the latter happens to be my `Leader` key. Thus, instead of getting the
following with `Space-tilde`:

    `some code that should be inline`

I am getting the three-tilde-enclosed code block as above. So I decided to
remove the `Leader-tilde` mapping in insert mode.

I source my vimrc through my shortcut:

{% gist f565fde6d384df819c6c %}

I do `:imap` to see all the insert mappings. However, the mapping is still
there.

    i  <Space>`   *@``````<Esc>2hi

I then tried clearing the insert mappings and then again sourcing the vimrc.
That still did not do the trick. I looked back at the old mapping and realized
that the mapping I removed has `<buffer>` in it. I looked up the help for
`imapclear` and found out that it can take `<buffer>` as an argument. I did:

    :imapclear <buffer>

That removed the mapping completely.

