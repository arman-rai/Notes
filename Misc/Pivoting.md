# Network pivoting

![[Pasted image 20250821204044.png]]

### Using Meterpreter to pivot
If you are currently interacting with a Meterpreter session, you must first `background` it and then `route`
```
# Example usage
route [add/remove] subnet netmask [comm/sid]
```

### Socks Proxy
A socks proxy is an intermediate server that supports relaying networking traffic between two machines using `auxiliary/server/socks_proxy`

If the tool does not natively support an option for using a socks proxy, ProxyChains can intercept the tool’s request to open new network connections and route the request through a socks proxy instead. For instance, an example with Nmap:
````
proxychains -q nmap -n -sT -Pn -p 22,80,443,5432 10.201.65.254
````
