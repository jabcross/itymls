# itymls — "i think you mean ls"

For stupid people like me.
Works even if you have `cat` aliased to something else.

```sh
alias cat='bat -p'
alias wkill='/usr/local/bin/WaylandReaper.sh'

oldCat=cat
if old=$(alias cat 2>/dev/null) ; then   # outputs `cat='<your alias>'`
  oldCat=$(alias cat | sed -E "s/^.*='?([^']*)'?$/\1/") # removes label and quotes
  unalias cat
fi

itymls() {
  if [ -d "$1" ]; then
    printf '\033[1;33mI think you mean ls:\033[0m\n'
    ls "$@"
  else
    eval "$oldCat" '"$@"'
  fi
}

alias cat=itymls

```

