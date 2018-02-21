# Ansible firewalld role 

simple ansible role for configuring firewalld

# Example

---

	- hosts:
	    - localhost
	  tasks:
	    - name: ping
	      ping:
	  roles:
	    - role: firewalld
	      firewalld_zones:
	        - name: public
	          description: For use in public areas. You do not trust the other computers on networks to not harm your 	computer. Only selected incoming connections are accepted.
	          interfaces: 
	            - wlp3s0
	          # sources:
	          ports:
	            - 1080/tcp
	          services:
	            - http
	            - https
	            - smtp
	            - dns
	            - ssh
	        - name: network2
	          description: description about network2
	          sources:
	            - address: 192.168.2.0/24
	            - address: 10.0.0.0/8
	          services:
	            - ssh
	            - dhcpv6-client
	            - https
	      firewalld_directs:
	        - table: filter
	          ipv: ipv4
	          priority: 10
	          chain: INPUT
	          rule: "-d 192.168.2.0/24 -j LOG"
	      firewalld_masquerade: no


