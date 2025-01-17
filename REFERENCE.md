# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

#### Public Classes

* [`firewall`](#firewall): Performs the basic setup tasks required for using the firewall resources.  At the moment this takes care of:  iptables-persistent package ins

#### Private Classes

* `firewall::linux`: Main linux class, includes all other classes
* `firewall::linux::archlinux`: Manages `iptables` and `ip6tables` services, and creates files used for persistence, on Arch Linux systems.
* `firewall::linux::debian`: Installs the `iptables-persistent` package for Debian-alike systems. This allows rules to be stored to file and restored on boot.
* `firewall::linux::gentoo`: Manages `iptables` and `ip6tables` services, and creates files used for persistence, on Gentoo Linux systems.
* `firewall::linux::redhat`: Manages the `iptables` service on RedHat-alike systems.
* `firewall::params`: Provides defaults for the Apt module parameters.

### Resource types

* [`firewall`](#firewall): This type provides the capability to manage firewall rules within puppet.
* [`firewallchain`](#firewallchain): This type provides the capability to manage rule chains for firewalls.

## Classes

### <a name="firewall"></a>`firewall`

Performs the basic setup tasks required for using the firewall resources.

At the moment this takes care of:

iptables-persistent package installation
Include the firewall class for nodes that need to use the resources in this module:

#### Examples

##### 

```puppet
class { 'firewall': }
```

#### Parameters

The following parameters are available in the `firewall` class:

* [`ensure`](#ensure)
* [`ensure_v6`](#ensure_v6)
* [`pkg_ensure`](#pkg_ensure)
* [`service_name`](#service_name)
* [`service_name_v6`](#service_name_v6)
* [`package_name`](#package_name)
* [`ebtables_manage`](#ebtables_manage)

##### <a name="ensure"></a>`ensure`

Data type: `Any`

Controls the state of the ipv4 iptables service on your system. Valid options: 'running' or 'stopped'.

Default value: `running`

##### <a name="ensure_v6"></a>`ensure_v6`

Data type: `Any`

Controls the state of the ipv6 iptables service on your system. Valid options: 'running' or 'stopped'.

Default value: ``undef``

##### <a name="pkg_ensure"></a>`pkg_ensure`

Data type: `Any`

Controls the state of the iptables package on your system. Valid options: 'present' or 'latest'.

Default value: `present`

##### <a name="service_name"></a>`service_name`

Data type: `Any`

Specify the name of the IPv4 iptables service.

Default value: `$firewall::params::service_name`

##### <a name="service_name_v6"></a>`service_name_v6`

Data type: `Any`

Specify the name of the IPv6 iptables service.

Default value: `$firewall::params::service_name_v6`

##### <a name="package_name"></a>`package_name`

Data type: `Any`

Specify the platform-specific package(s) to install.

Default value: `$firewall::params::package_name`

##### <a name="ebtables_manage"></a>`ebtables_manage`

Data type: `Any`

Controls whether puppet manages the ebtables package or not. If managed, the package will use the value of pkg_ensure.

Default value: ``false``

## Resource types

### <a name="firewall"></a>`firewall`

**Autorequires:**

If Puppet is managing the iptables or ip6tables chains specified in the
`chain` or `jump` parameters, the firewall resource will autorequire
those firewallchain resources.

If Puppet is managing the iptables, iptables-persistent, or iptables-services packages,
and the provider is iptables or ip6tables, the firewall resource will
autorequire those packages to ensure that any required binaries are
installed.

#### Providers
  Note: Not all features are available with all providers.

  * ip6tables: Ip6tables type provider

    * Required binaries: ip6tables-save, ip6tables.
    * Supported features: address_type, connection_limiting, conntrack, dnat, hop_limiting, icmp_match,
    interface_match, iprange, ipsec_dir, ipsec_policy, ipset, iptables, isfirstfrag,
    ishasmorefrags, islastfrag, length, log_level, log_prefix, log_uid,
    log_tcp_sequence, log_tcp_options, log_ip_options, mask, mss,
    owner, pkttype, queue_bypass, queue_num, rate_limiting, recent_limiting, reject_type,
    snat, socket, state_match, string_matching, tcp_flags, hashlimit, bpf.

  * iptables: Iptables type provider

    * Required binaries: iptables-save, iptables.
    * Default for kernel == linux.
    * Supported features: address_type, clusterip, connection_limiting, conntrack, dnat, icmp_match,
    interface_match, iprange, ipsec_dir, ipsec_policy, ipset, iptables, isfragment, length,
    log_level, log_prefix, log_uid, log_tcp_sequence, log_tcp_options, log_ip_options,
    mark, mask, mss, netmap, nfacct, nflog_group, nflog_prefix,
    nflog_range, nflog_threshold, owner, pkttype, queue_bypass, queue_num, rate_limiting,
    recent_limiting, reject_type, snat, socket, state_match, string_matching, tcp_flags, bpf.

#### Features
  * address_type: The ability to match on source or destination address type.

  * clusterip: Configure a simple cluster of nodes that share a certain IP and MAC address without an explicit load balancer in front of them.

  * condition: Match if a specific condition variable is (un)set (requires xtables-addons)

  * connection_limiting: Connection limiting features.

  * conntrack: Connection tracking features.

  * dnat: Destination NATing.

  * hop_limiting: Hop limiting features.

  * icmp_match: The ability to match ICMP types.

  * interface_match: Interface matching.

  * iprange: The ability to match on source or destination IP range.

  * ipsec_dir: The ability to match IPsec policy direction.

  * ipsec_policy: The ability to match IPsec policy.

  * iptables: The provider provides iptables features.

  * isfirstfrag: The ability to match the first fragment of a fragmented ipv6 packet.

  * isfragment: The ability to match fragments.

  * ishasmorefrags: The ability to match a non-last fragment of a fragmented ipv6 packet.

  * islastfrag: The ability to match the last fragment of an ipv6 packet.

  * length: The ability to match the length of the layer-3 payload.

  * log_level: The ability to control the log level.

  * log_prefix: The ability to add prefixes to log messages.

  * log_uid: The ability to log the userid of the process which generated the packet.

  * log_tcp_sequence: The ability to log TCP sequence numbers.

  * log_tcp_options: The ability to log TCP packet header.

  * log_ip_options: The ability to log IP/IPv6 packet header.

  * mark: The ability to match or set the netfilter mark value associated with the packet.

  * mask: The ability to match recent rules based on the ipv4 mask.

  * nfacct: The ability to increment nfacct(8) counters for matched packets.

  * nflog_group: The ability to set the group number for NFLOG.

  * nflog_prefix: The ability to set a prefix for nflog messages.

  * nflog_range: The ability to set nflog_range.

  * nflog_threshold: The ability to set nflog_threshold.

  * owner: The ability to match owners.

  * pkttype: The ability to match a packet type.

  * rate_limiting: Rate limiting features.

  * recent_limiting: The netfilter recent module.

  * reject_type: The ability to control reject messages.

  * set_mss: Set the TCP MSS of a packet.

  * snat: Source NATing.

  * socket: The ability to match open sockets.

  * state_match: The ability to match stateful firewall states.

  * string_matching: The ability to match a given string by using some pattern matching strategy.

  * tcp_flags: The ability to match on particular TCP flag settings.

  * netmap: The ability to map entire subnets via source or destination nat rules.

  * hashlimit: The ability to use the hashlimit-module.

  * bpf: The ability to use Berkeley Paket Filter rules.

  * ipvs: The ability to match IP Virtual Server packets.

  * ct_target: The ability to set connection tracking parameters for a packet or its associated connection.

  * random_fully: The ability to use --random-fully flag.

#### Properties

The following properties are available in the `firewall` type.

##### `action`

Valid values: `accept`, `reject`, `drop`

This is the action to perform on a match. Can be one of:

* accept - the packet is accepted
* reject - the packet is rejected with a suitable ICMP response
* drop - the packet is dropped

If you specify no value it will simply match the rule but perform no
action unless you provide a provider specific parameter (such as *jump*).

##### `burst`

Valid values: `%r{^\d+$}`

Rate limiting burst value (per second) before limit checks apply.

##### `bytecode`

Match using Linux Socket Filter. Expects a BPF program in decimal format.
This is the format generated by the nfbpf_compile utility.

##### `cgroup`

Matches against the net_cls cgroup ID of the packet.

##### `chain`

Valid values: `%r{^[a-zA-Z0-9\-_]+$}`

Name of the chain to use. Can be one of the built-ins:

* INPUT
* FORWARD
* OUTPUT
* PREROUTING
* POSTROUTING

Or you can provide a user-based chain.

Default value: `INPUT`

##### `checksum_fill`

Valid values: ``true``, ``false``

Compute and fill missing packet checksums.

##### `clamp_mss_to_pmtu`

Valid values: ``true``, ``false``

Sets the clamp mss to pmtu flag.

##### `clusterip_clustermac`

Valid values: `%r{^([0-9a-f]{2}[:]){5}([0-9a-f]{2})$}i`

Used with the CLUSTERIP jump target.
Specify the ClusterIP MAC address. Has to be a link-layer multicast address.

##### `clusterip_hash_init`

Used with the CLUSTERIP jump target.
Specify the random seed used for hash initialization.

##### `clusterip_hashmode`

Valid values: `sourceip`, `sourceip-sourceport`, `sourceip-sourceport-destport`

Used with the CLUSTERIP jump target.
Specify the hashing mode.

##### `clusterip_local_node`

Valid values: `%r{\d+}`

Used with the CLUSTERIP jump target.
Specify the random seed used for hash initialization.

##### `clusterip_new`

Valid values: ``true``, ``false``

Used with the CLUSTERIP jump target.
Create a new ClusterIP. You always have to set this on the first rule for a given ClusterIP.

##### `clusterip_total_nodes`

Valid values: `%r{\d+}`

Used with the CLUSTERIP jump target.
Number of total nodes within this cluster.

##### `condition`

Match on boolean value (0/1) stored in /proc/net/nf_condition/name.

##### `connlimit_above`

Valid values: `%r{^\d+$}`

Connection limiting value for matched connections above n.

##### `connlimit_mask`

Valid values: `%r{^\d+$}`

Connection limiting by subnet mask for matched connections.
IPv4: 0-32
IPv6: 0-128

##### `connmark`

Match the Netfilter mark value associated with the packet.  Accepts either of:
mark/mask or mark.  These will be converted to hex if they are not already.

##### `ctdir`

Valid values: `REPLY`, `ORIGINAL`

Matches a packet that is flowing in the specified direction using the
conntrack module. If this flag is not specified at all, matches packets
in both directions. Values can be:

* REPLY
* ORIGINAL

##### `ctexpire`

Valid values: `%r{^!?\s?\d+$|^!?\s?\d+\:\d+$}`

Matches a packet based on lifetime remaining in seconds or range of values
using the conntrack module. For example:

    ctexpire => '100:150'

##### `ctorigdst`

The original destination address using the conntrack module. For example:

    ctorigdst => '192.168.2.0/24'

You can also negate a mask by putting ! in front. For example:

    ctorigdst => '! 192.168.2.0/24'

The ctorigdst can also be an IPv6 address if your provider supports it.

##### `ctorigdstport`

Valid values: `%r{^!?\s?\d+$|^!?\s?\d+\:\d+$}`

The original destination port to match for this filter using the conntrack module.
For example:

    ctorigdstport => '80'

You can also specify a port range: For example:

    ctorigdstport => '80:81'

You can also negate a port by putting ! in front. For example:

    ctorigdstport => '! 80'

##### `ctorigsrc`

The original source address using the conntrack module. For example:

    ctorigsrc => '192.168.2.0/24'

You can also negate a mask by putting ! in front. For example:

    ctorigsrc => '! 192.168.2.0/24'

The ctorigsrc can also be an IPv6 address if your provider supports it.

##### `ctorigsrcport`

Valid values: `%r{^!?\s?\d+$|^!?\s?\d+\:\d+$}`

The original source port to match for this filter using the conntrack module.
For example:

    ctorigsrcport => '80'

You can also specify a port range: For example:

    ctorigsrcport => '80:81'

You can also negate a port by putting ! in front. For example:

    ctorigsrcport => '! 80'

##### `ctproto`

Valid values: `%r{^!?\s?\d+$}`

The specific layer-4 protocol number to match for this rule using the
conntrack module.

##### `ctrepldst`

The reply destination address using the conntrack module. For example:

    ctrepldst => '192.168.2.0/24'

You can also negate a mask by putting ! in front. For example:

    ctrepldst => '! 192.168.2.0/24'

The ctrepldst can also be an IPv6 address if your provider supports it.

##### `ctrepldstport`

Valid values: `%r{^!?\s?\d+$|^!?\s?\d+\:\d+$}`

The reply destination port to match for this filter using the conntrack module.
For example:

    ctrepldstport => '80'

You can also specify a port range: For example:

    ctrepldstport => '80:81'

You can also negate a port by putting ! in front. For example:

    ctrepldstport => '! 80'

##### `ctreplsrc`

The reply source address using the conntrack module. For example:

    ctreplsrc => '192.168.2.0/24'

You can also negate a mask by putting ! in front. For example:

    ctreplsrc => '! 192.168.2.0/24'

The ctreplsrc can also be an IPv6 address if your provider supports it.

##### `ctreplsrcport`

Valid values: `%r{^!?\s?\d+$|^!?\s?\d+\:\d+$}`

The reply source port to match for this filter using the conntrack module.
For example:

    ctreplsrcport => '80'

You can also specify a port range: For example:

    ctreplsrcport => '80:81'

You can also negate a port by putting ! in front. For example:

    ctreplsrcport => '! 80'

##### `ctstate`

Valid values: `INVALID`, `ESTABLISHED`, `NEW`, `RELATED`, `UNTRACKED`, `SNAT`, `DNAT`

Matches a packet based on its state in the firewall stateful inspection
table, using the conntrack module. Values can be:

* INVALID
* ESTABLISHED
* NEW
* RELATED
* UNTRACKED
* SNAT
* DNAT

##### `ctstatus`

Valid values: `NONE`, `EXPECTED`, `SEEN_REPLY`, `ASSURED`, `CONFIRMED`

Matches a packet based on its status using the conntrack module. Values can be:

* EXPECTED
* SEEN_REPLY
* ASSURED
* CONFIRMED

##### `date_start`

Only match during the given time, which must be in ISO 8601 "T" notation.
The possible time range is 1970-01-01T00:00:00 to 2038-01-19T04:17:07

##### `date_stop`

Only match during the given time, which must be in ISO 8601 "T" notation.
The possible time range is 1970-01-01T00:00:00 to 2038-01-19T04:17:07

##### `destination`

The destination address to match. For example:

    destination => '192.168.1.0/24'

You can also negate a mask by putting ! in front. For example:

    destination  => '! 192.168.2.0/24'

The destination can also be an IPv6 address if your provider supports it.

##### `dport`

The destination port to match for this filter (if the protocol supports
ports). Will accept a single element or an array.

For some firewall providers you can pass a range of ports in the format:

    <start_number>-<ending_number>

For example:

    1-1024

This would cover ports 1 to 1024.

##### `dst_cc`

Valid values: `%r{^[A-Z]{2}(,[A-Z]{2})*$}`

dst attribute for the module geoip

##### `dst_range`

The destination IP range. For example:

    dst_range => '192.168.1.1-192.168.1.10'

The destination IP range must be in 'IP1-IP2' format.

##### `dst_type`

Valid values: `[:UNSPEC, :UNICAST, :LOCAL, :BROADCAST, :ANYCAST, :MULTICAST,
                :BLACKHOLE, :UNREACHABLE, :PROHIBIT, :THROW, :NAT, :XRESOLVE].map { |address_type|
                [
                  address_type,
                  "! #{address_type}".to_sym,
                  "#{address_type} --limit-iface-in".to_sym,
                  "#{address_type} --limit-iface-out".to_sym,
                  "! #{address_type} --limit-iface-in".to_sym,
                  "! #{address_type} --limit-iface-out".to_sym,
                ]
              }.flatten`

The destination address type. For example:

    dst_type => ['LOCAL']

Can be one of:

* UNSPEC - an unspecified address
* UNICAST - a unicast address
* LOCAL - a local address
* BROADCAST - a broadcast address
* ANYCAST - an anycast packet
* MULTICAST - a multicast address
* BLACKHOLE - a blackhole address
* UNREACHABLE - an unreachable address
* PROHIBIT - a prohibited address
* THROW - undocumented
* NAT - undocumented
* XRESOLVE - undocumented

In addition, it accepts '--limit-iface-in' and '--limit-iface-out' flags, specified as:

    dst_type => ['LOCAL --limit-iface-in']

It can also be negated using '!':

    dst_type => ['! LOCAL']

Will accept a single element or an array.

##### `ensure`

Valid values: `present`, `absent`

Manage the state of this rule.

Default value: `present`

##### `gateway`

The TEE target will clone a packet and redirect this clone to another
machine on the local network segment. gateway is the target host's IP.

##### `gid`

GID or Group owner matching rule.  Accepts a string argument
only, as iptables does not accept multiple gid in a single
statement.

##### `goto`

The value for the iptables --goto parameter. Normal values are:

* QUEUE
* RETURN
* DNAT
* SNAT
* LOG
* MASQUERADE
* REDIRECT
* MARK

But any valid chain name is allowed.

##### `hashlimit_above`

Match if the rate is above amount/quantum.
This parameter or hashlimit_upto is required.
Allowed forms are '40','40/second','40/minute','40/hour','40/day'.

##### `hashlimit_burst`

Valid values: `%r{^\d+$}`

Maximum initial number of packets to match: this number gets recharged by one every time the limit specified above is not reached, up to this number; the default is 5. When byte-based rate matching is requested, this option specifies the amount of bytes that can exceed the given rate. This option should be used with caution -- if the entry expires, the burst value is reset too.

##### `hashlimit_dstmask`

Like --hashlimit-srcmask, but for destination addresses.

##### `hashlimit_htable_expire`

After how many milliseconds do hash entries expire.

##### `hashlimit_htable_gcinterval`

How many milliseconds between garbage collection intervals.

##### `hashlimit_htable_max`

Maximum entries in the hash.

##### `hashlimit_htable_size`

The number of buckets of the hash table

##### `hashlimit_mode`

A comma-separated list of objects to take into consideration. If no --hashlimit-mode option is given, hashlimit acts like limit, but at the expensive of doing the hash housekeeping.
Allowed values are: srcip, srcport, dstip, dstport

##### `hashlimit_name`

The name for the /proc/net/ipt_hashlimit/foo entry.
This parameter is required.

##### `hashlimit_srcmask`

When --hashlimit-mode srcip is used, all source addresses encountered will be grouped according to the given prefix length and the so-created subnet will be subject to hashlimit. prefix must be between (inclusive) 0 and 32. Note that --hashlimit-srcmask 0 is basically doing the same thing as not specifying srcip for --hashlimit-mode, but is technically more expensive.

##### `hashlimit_upto`

Match if the rate is below or equal to amount/quantum. It is specified either as a number, with an optional time quantum suffix (the default is 3/hour), or as amountb/second (number of bytes per second).
This parameter or hashlimit_above is required.
Allowed forms are '40','40/second','40/minute','40/hour','40/day'.

##### `helper`

Invoke the nf_conntrack_xxx helper module for this packet.

##### `hop_limit`

Valid values: `%r{^\d+$}`

Hop limiting value for matched packets.

##### `icmp`

When matching ICMP packets, this is the type of ICMP packet to match.

A value of "any" is not supported. To achieve this behaviour the
parameter should simply be omitted or undefined.
An array of values is also not supported. To match against multiple ICMP
types, please use separate rules for each ICMP type.

##### `iniface`

Valid values: `%r{^!?\s?[a-zA-Z0-9\-\._\+\:@]+$}`

Input interface to filter on.  Supports interface alias like eth0:0.
To negate the match try this:

      iniface => '! lo',

##### `ipsec_dir`

Valid values: `in`, `out`

Sets the ipsec policy direction

##### `ipsec_policy`

Valid values: `none`, `ipsec`

Sets the ipsec policy type. May take a combination of arguments for any flags that can be passed to `--pol ipsec` such as: `--strict`, `--reqid 100`, `--next`, `--proto esp`, etc.

##### `ipset`

Matches against the specified ipset list.
Requires ipset kernel module. Will accept a single element or an array.
The value is the name of the blacklist, followed by a space, and then
'src' and/or 'dst' separated by a comma.
For example: 'blacklist src,dst'

##### `ipvs`

Valid values: ``true``, ``false``

Indicates that the current packet belongs to an IPVS connection.

##### `isfirstfrag`

Valid values: ``true``, ``false``

If true, matches if the packet is the first fragment.
Sadly cannot be negated. ipv6.

##### `isfragment`

Valid values: ``true``, ``false``

Set to true to match tcp fragments (requires type to be set to tcp)

##### `ishasmorefrags`

Valid values: ``true``, ``false``

If true, matches if the packet has it's 'more fragments' bit set. ipv6.

##### `islastfrag`

Valid values: ``true``, ``false``

If true, matches if the packet is the last fragment. ipv6.

##### `jump`

The value for the iptables --jump parameter. Normal values are:

* QUEUE
* RETURN
* DNAT
* SNAT
* LOG
* NFLOG
* MASQUERADE
* REDIRECT
* MARK
* CT

But any valid chain name is allowed.

For the values ACCEPT, DROP, and REJECT, you must use the generic
'action' parameter. This is to enfore the use of generic parameters where
possible for maximum cross-platform modelling.

If you set both 'accept' and 'jump' parameters, you will get an error as
only one of the options should be set.

##### `kernel_timezone`

Valid values: ``true``, ``false``

Use the kernel timezone instead of UTC to determine whether a packet meets the time regulations.

##### `length`

Sets the length of layer-3 payload to match.

##### `limit`

Rate limiting value for matched packets. The format is:
rate/[/second/|/minute|/hour|/day].

Example values are: '50/sec', '40/min', '30/hour', '10/day'."

##### `log_ip_options`

Valid values: ``true``, ``false``

When combined with jump => "LOG" logging of the TCP IP/IPv6
packet header.

##### `log_level`

When combined with jump => "LOG" specifies the system log level to log
to.

##### `log_prefix`

When combined with jump => "LOG" specifies the log prefix to use when
logging.

##### `log_tcp_options`

Valid values: ``true``, ``false``

When combined with jump => "LOG" logging of the TCP packet
header.

##### `log_tcp_sequence`

Valid values: ``true``, ``false``

When combined with jump => "LOG" enables logging of the TCP sequence
numbers.

##### `log_uid`

Valid values: ``true``, ``false``

When combined with jump => "LOG" specifies the uid of the process making
the connection.

##### `mac_source`

Valid values: `%r{^([0-9a-f]{2}[:]){5}([0-9a-f]{2})$}i`

MAC Source

##### `mask`

Sets the mask to use when `recent` is enabled.

##### `match_mark`

Match the Netfilter mark value associated with the packet.  Accepts either of:
mark/mask or mark.  These will be converted to hex if they are not already.

##### `month_days`

Only match on the given days of the month. Possible values are 1 to 31.
Note that specifying 31 will of course not match on months which do not have a 31st day;
the same goes for 28- or 29-day February.

##### `mss`

Match a given TCP MSS value or range.

##### `nfacct`

Match any packet with other named properties and increment the named counter.
The counter must have already been set up with nfacct(8).

##### `nflog_group`

Used with the jump target NFLOG.
The netlink group (0 - 2^16-1) to which packets are (only applicable
for nfnetlink_log). Defaults to 0.

##### `nflog_prefix`

Used with the jump target NFLOG.
A prefix string to include in the log message, up to 64 characters long,
useful for distinguishing messages in the logs.

##### `nflog_range`

Used with the jump target NFLOG.
The number of bytes to be copied to userspace (only applicable for nfnetlink_log).
nfnetlink_log instances may specify their own range, this option overrides it.

##### `nflog_threshold`

Used with the jump target NFLOG.
Number of packets to queue inside the kernel before sending them to userspace
(only applicable for nfnetlink_log). Higher values result in less overhead
per packet, but increase delay until the packets reach userspace. Defaults to 1.

##### `notrack`

Valid values: ``true``, ``false``

Invoke the disable connection tracking for this packet.
This parameter can be used with iptables version >= 1.8.3

##### `outiface`

Valid values: `%r{^!?\s?[a-zA-Z0-9\-\._\+\:@]+$}`

 Output interface to filter on.  Supports interface alias like eth0:0.
To negate the match try this:

      outiface => '! lo',

##### `physdev_in`

Valid values: `%r{^[a-zA-Z0-9\-\._\+]+$}`

Match if the packet is entering a bridge from the given interface.

##### `physdev_is_bridged`

Valid values: ``true``, ``false``

Match if the packet is transversing a bridge.

##### `physdev_is_in`

Valid values: ``true``, ``false``

Matches if the packet has entered through a bridge interface.

##### `physdev_is_out`

Valid values: ``true``, ``false``

Matches if the packet will leave through a bridge interface.

##### `physdev_out`

Valid values: `%r{^[a-zA-Z0-9\-\._\+]+$}`

Match if the packet is leaving a bridge via the given interface.

##### `pkttype`

Valid values: `unicast`, `broadcast`, `multicast`

Sets the packet type to match.

##### `port`

*note* This property has been DEPRECATED

The destination or source port to match for this filter (if the protocol
supports ports). Will accept a single element or an array.

For some firewall providers you can pass a range of ports in the format:

    <start_number>-<ending_number>

For example:

    1-1024

This would cover ports 1 to 1024.

##### `proto`

Valid values: `[:ip, :tcp, :udp, :icmp, :"ipv6-icmp", :esp, :ah, :vrrp, :carp, :igmp, :ipencap, :ipv4, :ipv6, :ospf, :gre, :cbt, :sctp, :pim, :all].map { |proto|
      [proto, "! #{proto}".to_sym]
    }.flatten`

The specific protocol to match for this rule.

Default value: `tcp`

##### `queue_bypass`

Valid values: ``true``, ``false``

Used with NFQUEUE jump target
Allow packets to bypass :queue_num if userspace process is not listening

##### `queue_num`

Used with NFQUEUE jump target.
What queue number to send packets to

##### `random`

Valid values: ``true``, ``false``

When using a jump value of "MASQUERADE", "DNAT", "REDIRECT", or "SNAT"
this boolean will enable randomized port mapping.

##### `random_fully`

Valid values: ``true``, ``false``

When using a jump value of "MASQUERADE", "DNAT", "REDIRECT", or "SNAT"
this boolean will enable fully randomized port mapping.

**NOTE** Requires Kernel >= 3.13 and iptables >= 1.6.2

##### `rdest`

Valid values: ``true``, ``false``

Recent module; add the destination IP address to the list.
Must be boolean true.

##### `reap`

Valid values: ``true``, ``false``

Recent module; can only be used in conjunction with the `rseconds`
attribute. When used, this will cause entries older than 'seconds' to be
purged.  Must be boolean true.

##### `recent`

Valid values: `set`, `update`, `rcheck`, `remove`

Enable the recent module. Takes as an argument one of set, update,
rcheck or remove. For example:

  ```
  # If anyone's appeared on the 'badguy' blacklist within
  #  the last 60 seconds, drop their traffic, and update the timestamp.
  firewall { '100 Drop badguy traffic':
    recent   => 'update',
    rseconds => 60,
    rsource  => true,
    rname    => 'badguy',
    action   => 'DROP',
    chain    => 'FORWARD',
  }
  ```


  ```
  # No-one should be sending us traffic on eth0 from the
  #  localhost, Blacklist them
  firewall { '101 blacklist strange traffic':
    recent      => 'set',
    rsource     => true,
    rname       => 'badguy',
    destination => '127.0.0.0/8',
    iniface     => 'eth0',
    action      => 'DROP',
    chain       => 'FORWARD',
  }
  ```

##### `reject`

When combined with action => "REJECT" you can specify a different icmp
response to be sent back to the packet sender.

##### `rhitcount`

Recent module; used in conjunction with `recent => 'update'` or `recent
=> 'rcheck'. When used, this will narrow the match to only happen when
the address is in the list and packets had been received greater than or
equal to the given value.

##### `rname`

Recent module; The name of the list. Takes a string argument.

##### `rpfilter`

Valid values: `loose`, `validmark`, `accept-local`, `invert`

Enable the rpfilter module.

##### `rseconds`

Recent module; used in conjunction with one of `recent => 'rcheck'` or
`recent => 'update'`. When used, this will narrow the match to only
happen when the address is in the list and was seen within the last given
number of seconds.

##### `rsource`

Valid values: ``true``, ``false``

Recent module; add the source IP address to the list.
Must be boolean true.

##### `rttl`

Valid values: ``true``, ``false``

Recent module; may only be used in conjunction with one of `recent =>
'rcheck'` or `recent => 'update'`. When used, this will narrow the match
to only happen when the address is in the list and the TTL of the current
packet matches that of the packet which hit the `recent => 'set'` rule.
This may be useful if you have problems with people faking their source
address in order to DoS you via this module by disallowing others access
to your site by sending bogus packets to you.  Must be boolean true.

##### `set_dscp`

Set DSCP Markings.

##### `set_dscp_class`

This sets the DSCP field according to a predefined DiffServ class.

##### `set_mark`

Set the Netfilter mark value associated with the packet.  Accepts either of:
mark/mask or mark.  These will be converted to hex if they are not already.

##### `set_mss`

Sets the TCP MSS value for packets.

##### `socket`

Valid values: ``true``, ``false``

If true, matches if an open socket can be found by doing a coket lookup
on the packet.

##### `source`

The source address. For example:

    source => '192.168.2.0/24'

You can also negate a mask by putting ! in front. For example:

    source => '! 192.168.2.0/24'

The source can also be an IPv6 address if your provider supports it.

##### `sport`

The source port to match for this filter (if the protocol supports
ports). Will accept a single element or an array.

For some firewall providers you can pass a range of ports in the format:

    <start_number>-<ending_number>

For example:

    1-1024

This would cover ports 1 to 1024.

##### `src_cc`

Valid values: `%r{^[A-Z]{2}(,[A-Z]{2})*$}`

src attribute for the module geoip

##### `src_range`

The source IP range. For example:

    src_range => '192.168.1.1-192.168.1.10'

The source IP range must be in 'IP1-IP2' format.

##### `src_type`

Valid values: `[:UNSPEC, :UNICAST, :LOCAL, :BROADCAST, :ANYCAST, :MULTICAST,
                :BLACKHOLE, :UNREACHABLE, :PROHIBIT, :THROW, :NAT, :XRESOLVE].map { |address_type|
                [
                  address_type,
                  "! #{address_type}".to_sym,
                  "#{address_type} --limit-iface-in".to_sym,
                  "#{address_type} --limit-iface-out".to_sym,
                  "! #{address_type} --limit-iface-in".to_sym,
                  "! #{address_type} --limit-iface-out".to_sym,
                ]
              }.flatten`

The source address type. For example:

    src_type => ['LOCAL']

Can be one of:

* UNSPEC - an unspecified address
* UNICAST - a unicast address
* LOCAL - a local address
* BROADCAST - a broadcast address
* ANYCAST - an anycast packet
* MULTICAST - a multicast address
* BLACKHOLE - a blackhole address
* UNREACHABLE - an unreachable address
* PROHIBIT - a prohibited address
* THROW - undocumented
* NAT - undocumented
* XRESOLVE - undocumented

In addition, it accepts '--limit-iface-in' and '--limit-iface-out' flags, specified as:

    src_type => ['LOCAL --limit-iface-in']

It can also be negated using '!':

    src_type => ['! LOCAL']

Will accept a single element or an array.

##### `stat_every`

Match one packet every nth packet. Requires `stat_mode => 'nth'`

##### `stat_mode`

Valid values: `nth`, `random`

Set the matching mode for statistic matching.

##### `stat_packet`

Valid values: `%r{^\d+$}`

Set the initial counter value for the nth mode. Must be between 0 and the value of `stat_every`. Defaults to 0. Requires `stat_mode => 'nth'`

##### `stat_probability`

Set the probability from 0 to 1 for a packet to be randomly matched. It works only with `stat_mode => 'random'`.

##### `state`

Valid values: `INVALID`, `ESTABLISHED`, `NEW`, `RELATED`, `UNTRACKED`

Matches a packet based on its state in the firewall stateful inspection
table. Values can be:

* INVALID
* ESTABLISHED
* NEW
* RELATED
* UNTRACKED

##### `string`

String matching feature. Matches the packet against the pattern
given as an argument.

##### `string_algo`

Valid values: `bm`, `kmp`

String matching feature, pattern matching strategy.

##### `string_from`

String matching feature, offset from which we start looking for any matching.

##### `string_hex`

String matching feature. Matches the package against the hex pattern
given as an argument.

##### `string_to`

String matching feature, offset up to which we should scan.

##### `table`

Valid values: `nat`, `mangle`, `filter`, `raw`, `rawpost`

Table to use. Can be one of:

* nat
* mangle
* filter
* raw
* rawpost

Default value: `filter`

##### `tcp_flags`

Match when the TCP flags are as specified.
Is a string with a list of comma-separated flag names for the mask,
then a space, then a comma-separated list of flags that should be set.
The flags are: SYN ACK FIN RST URG PSH ALL NONE
Note that you specify them in the order that iptables --list-rules
would list them to avoid having puppet think you changed the flags.
Example: FIN,SYN,RST,ACK SYN matches packets with the SYN bit set and the
ACK,RST and FIN bits cleared. Such packets are used to request
TCP  connection initiation.

##### `time_contiguous`

Valid values: ``true``, ``false``

When time_stop is smaller than time_start value, match this as a single time period instead distinct intervals.

##### `time_start`

Only match during the given daytime. The possible time range is 00:00:00 to 23:59:59.
Leading zeroes are allowed (e.g. "06:03") and correctly interpreted as base-10.

##### `time_stop`

Only match during the given daytime. The possible time range is 00:00:00 to 23:59:59.
Leading zeroes are allowed (e.g. "06:03") and correctly interpreted as base-10.

##### `to`

For NETMAP this will replace the destination IP

##### `todest`

When using jump => "DNAT" you can specify the new destination address
using this paramter.

##### `toports`

For DNAT this is the port that will replace the destination port.

##### `tosource`

When using jump => "SNAT" you can specify the new source address using
this parameter.

##### `uid`

UID or Username owner matching rule.  Accepts a string argument
only, as iptables does not accept multiple uid in a single
statement.

##### `week_days`

Valid values: `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`

Only match on the given weekdays.

##### `zone`

Assign this packet to zone id and only have lookups done in that zone.

#### Parameters

The following parameters are available in the `firewall` type.

* [`line`](#line)
* [`name`](#name)
* [`provider`](#provider)

##### <a name="line"></a>`line`

Read-only property for caching the rule line.

##### <a name="name"></a>`name`

Valid values: `%r{^\d+[[:graph:][:space:]]+$}`

namevar

The canonical name of the rule. This name is also used for ordering
so make sure you prefix the rule with a number:

    000 this runs first
    999 this runs last

Depending on the provider, the name of the rule can be stored using
the comment feature of the underlying firewall subsystem.

##### <a name="provider"></a>`provider`

The specific backend to use for this `firewall` resource. You will seldom need to specify this --- Puppet will usually
discover the appropriate provider for your platform.

### <a name="firewallchain"></a>`firewallchain`

Currently this supports only iptables, ip6tables and ebtables on Linux. And
provides support for setting the default policy on chains and tables that
allow it.

**Autorequires:**
If Puppet is managing the iptables, iptables-persistent, or iptables-services packages,
and the provider is iptables_chain, the firewall resource will autorequire
those packages to ensure that any required binaries are installed.

#### Providers
  * iptables_chain is the only provider that supports firewallchain.

#### Features
  * iptables_chain: The provider provides iptables chain features.
  * policy: Default policy (inbuilt chains only).

#### Properties

The following properties are available in the `firewallchain` type.

##### `ensure`

Valid values: `present`, `absent`

The basic property that the resource should be in.

Default value: `present`

##### `policy`

Valid values: `accept`, `drop`, `queue`, `return`

This is the action to when the end of the chain is reached.
It can only be set on inbuilt chains (INPUT, FORWARD, OUTPUT,
PREROUTING, POSTROUTING) and can be one of:

* accept - the packet is accepted
* drop - the packet is dropped
* queue - the packet is passed userspace
* return - the packet is returned to calling (jump) queue
           or the default of inbuilt chains

#### Parameters

The following parameters are available in the `firewallchain` type.

* [`ignore`](#ignore)
* [`ignore_foreign`](#ignore_foreign)
* [`name`](#name)
* [`provider`](#provider)
* [`purge`](#purge)

##### <a name="ignore"></a>`ignore`

Regex to perform on firewall rules to exempt unmanaged rules from purging (when enabled).
This is matched against the output of `iptables-save`.

This can be a single regex, or an array of them.
To support flags, use the ruby inline flag mechanism.
Meaning a regex such as
  /foo/i
can be written as
  '(?i)foo' or '(?i:foo)'

Full example:
```
firewallchain { 'INPUT:filter:IPv4':
  purge => true,
  ignore => [
    '-j fail2ban-ssh', # ignore the fail2ban jump rule
    '--comment "[^"]*(?i:ignore)[^"]*"', # ignore any rules with "ignore" (case insensitive) in the comment in the rule
  ],
}
```

##### <a name="ignore_foreign"></a>`ignore_foreign`

Valid values: ``false``, ``true``

Ignore rules that do not match the puppet title pattern "^\d+[[:graph:][:space:]]" when purging unmanaged firewall rules
in this chain.
This can be used to ignore rules that were not put in by puppet. Beware that nothing keeps other systems from
configuring firewall rules with a comment that starts with digits, and is indistinguishable from puppet-configured
rules.

Default value: ``false``

##### <a name="name"></a>`name`

namevar

The canonical name of the chain.

For iptables the format must be {chain}:{table}:{protocol}.

##### <a name="provider"></a>`provider`

The specific backend to use for this `firewallchain` resource. You will seldom need to specify this --- Puppet will
usually discover the appropriate provider for your platform.

##### <a name="purge"></a>`purge`

Valid values: ``false``, ``true``

Purge unmanaged firewall rules in this chain

Default value: ``false``

