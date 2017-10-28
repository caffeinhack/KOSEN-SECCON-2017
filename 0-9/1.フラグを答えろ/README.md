# フラグを答えろ
## 問題
> ### [Description]
> 正しいフラグを書けば正しいかどうかを判定してくれる、便利なアプリを開発した。
フラグを調べて解答せよ。  

> ### [Problem File]
>[https://score.kosensc2017.tech/contents/problem/0/a.out](https://raw.githubusercontent.com/caffeinhack/KOSEN-SECCON-2017/master/0-9/1.%E3%83%95%E3%83%A9%E3%82%B0%E3%82%92%E7%AD%94%E3%81%88%E3%82%8D/a.out)

## 解き方
指定のファイルをダウンロードして、stringsコマンドをかけるると以下のように表示されるのですが…
```
$ strings a.out
/lib64/ld-linux-x86-64.so.2
{e#yd
libc.so.6
puts
__stack_chk_fail
stdin
printf
strtok
fgets
strcmp
__libc_start_main
__gmon_start__
GLIBC_2.4
GLIBC_2.2.5
UH-`
SCKOSEN{H
h1dden_fH
1ag}
AWAVA
AUATL
[]A\A]A^A_
Enter the FLAG:
correct! the flag is %s
wrong flag.
;*3$"
GCC: (Ubuntu 5.4.0-6ubuntu1~16.04.5) 5.4.0 20160609
crtstuff.c
__JCR_LIST__
deregister_tm_clones
__do_global_dtors_aux
completed.7585
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
main.c
__FRAME_END__
__JCR_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@@GLIBC_2.2.5
stdin@@GLIBC_2.2.5
_edata
__stack_chk_fail@@GLIBC_2.4
printf@@GLIBC_2.2.5
__libc_start_main@@GLIBC_2.2.5
fgets@@GLIBC_2.2.5
__data_start
strcmp@@GLIBC_2.2.5
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
strtok@@GLIBC_2.2.5
_Jv_RegisterClasses
__TMC_END__
_ITM_registerTMCloneTable
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.jcr
.dynamic
.got.plt
.data
.bss
.comment
```

出力の16行目~19行目に以下の文字列が…
```
SCKOSEN{H
h1dden_fH
1ag}
```

ということで、改行を消して明らかに関係なさそうな`H`を取るとFlagゲット！
> SCKOSEN{h1dden_f1ag}
