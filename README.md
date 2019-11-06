

# Aria2 RPC #
```
aria2c --enable-rpc=true --input-file=~/.aria2/aria2.session --conf-path=~/.aria2/aria2.conf
```

# 更新tracker

curl -fs -C - \
    https://raw.githubusercontent.com/ngosang/trackerslist/master/{trackers_best,trackers_best_ip,trackers_all,trackers_all_http,trackers_all_https,trackers_all_udp,trackers_all_ws,trackers_all_ip}.txt \
    | sort -u | awk NF | gsed ':a;N;s/\n/,/g;ta' \
    | gxargs -r -n 1 -I '{}' \
    gsed -i '/^bt-tracker\=/{h;s#\(^bt-tracker\=\).*$#\1{}#};${x;/^$/{s##bt-tracker\={}#;H};x}' /usr/local/etc/aria2/aria2.conf