+++
title = "Editor"
author = ["Shawn Dennis Lin"]
date = 2021-09-09T00:00:00+08:00
draft = false
+++

## Emacs {#emacs}


### Action {#action}


#### Reload environment variables {#reload-environment-variables}

Step:  

1.  type `M-:` `(getenv "PATH")`
2.  Install package `exec-path-from-shell`
3.  Do below

<!--listend-->

```lisp
(exec-path-from-shell-initialize)
;; (exec-path-from-shell-copy-env)
```

Ref: [Reload environment variables](https://emacs.stackexchange.com/questions/6104/reload-environment-variables), [https://github.com/purcell/exec-path-from-shell](https://github.com/purcell/exec-path-from-shell)  


### Command {#command}

| key         | function                   | describe                                        |
|-------------|----------------------------|-------------------------------------------------|
| `C-c C-x \` | org-toggle-pretty-entities | Toggle display of entities as UTF-8 characters. |
|             |                            |                                                 |


### Problem {#problem}
