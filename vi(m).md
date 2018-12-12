## Replace

1. Uncomment debug statement, say `printf`. 
>  `:%s/\(printf.*\);/\/\*\1\*\//c`
