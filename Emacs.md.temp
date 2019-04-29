# Happy hack emacs

## 自定义快捷键

`(define-key keymap key def)`
keymap是key所属的集合
- 一个interactive function，即一个command，这也是键绑定最直接的方式。
- 一个key，仅对于keymap为'key-translation-map这种情况，意味着映射到另一个键。
- 一个keymap，通过这种方式用户可以自定义prefix key。
- 一个nil，代表注销这个key。
### 1.优先级最高：key-translation-map

`(define-key key-translation-map (kbd "your-key") (kbd "target-key"))`

**特点：由于映射键是完全的跳转到了另一个键上，所以一旦目标键的定义发生了变化，该键也会随之受到影响。**

注销方式：重新映射自己

### 2.优先级第二：minor-mode-map

`(define-key some-minor-mode-map (kbd "your-key") 'your-command)`

**特点：仅在minor-mode激活时有效，定义方便且优先级高，不用担心键冲突。**

注销方式：绑定为nil。

### 3.优先级第三：local-set-key

`(local-set-key (kbd "your-key") 'your-command)`

local-set-key主要是在各种major-mode下使用，一般是通过hook设置


`(add-hook 'some-major-mode-hook '(lambda () (local-set-key ...)))`

**特点：通过这种方式设置的键绑定仅在该major-mode下生效，不影响其他major-mode，实惠好用。**

注销方式：绑定为nil。或者  `(local-unset-key (kbd "your-key")`

### 4.优先级最低：global-set-key

`(global-set-key (kbd "your-key") 'your-command)`

**特点：最简单的键绑定方式，一行搞定，无须关心到底是哪个keymap。然而需小心在某些major-mode时会被覆盖。**

注销方式：绑定为nil，或者  `(global-unset-key (kbd "your-key")`
