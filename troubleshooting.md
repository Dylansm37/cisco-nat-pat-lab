## Troubleshooting

Initially, NAT translations appeared in the translation table, but the **inside global address** incorrectly showed `192.168.1.1` instead of the expected `203.0.113.1`.

Inspection of the running configuration revealed that the PAT command referenced `GigabitEthernet0/0` instead of `GigabitEthernet0/1`.

### Incorrect Configuration

The original command used the inside interface:

```cisco
ip nat inside source list 10 interface GigabitEthernet0/0 overload
```

### Corrected Configuration

The incorrect command was removed and replaced with the outside interface:

```cisco
no ip nat inside source list 10 interface GigabitEthernet0/0 overload
ip nat inside source list 10 interface GigabitEthernet0/1 overload
```

### Verification

After correcting the configuration, NAT translations displayed the expected inside global address of `203.0.113.1`.

This confirmed that PAT was correctly translating the private inside address to the IP address assigned to the router's outside interface.
