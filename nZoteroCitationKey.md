# Better BibTeX Zotero citation key

```
(authEtal2) ? (authEtal2 + year) : (shorttitle || date)
```

```
authors(max=2,sep='_') + '_' + year | authors(n=1,sep='_',etal=EtAl)+ '_' + year
```

```
authors(max=2,sep='_') + year | authors(n=1,sep='_',etal=EtAl) + year || (shorttitle || date)
```

https://retorque.re/zotero-better-bibtex/citing/

https://joshcarpenter.ca/plain-text-refs-mgmt/

https://forums.zotero.org/discussion/72529/zotero-2-machines-cite-keys-and-betterbibtex

```
authEtal2(creator='*', initials=false, sep='.') + year
```

```
(auth ? authEtal2(creator='*', initials=false, sep='.') + year : shorttitle + year)
```



### **date**(format='%Y-%m-%d')

### **origyear**

