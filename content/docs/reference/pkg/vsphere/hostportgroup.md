
---
title: "HostPortGroup"
block_external_search_index: true
---



The `vsphere..HostPortGroup` resource can be used to manage vSphere standard
port groups on an ESXi host. These port groups are connected to standard
virtual switches, which can be managed by the
[`vsphere..HostVirtualSwitch`][host-virtual-switch] resource.

For an overview on vSphere networking concepts, see [this page][ref-vsphere-net-concepts].

[host-virtual-switch]: /docs/providers/vsphere/r/host_virtual_switch.html
[ref-vsphere-net-concepts]: https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.networking.doc/GUID-2B11DBB8-CB3C-4AFF-8885-EFEA0FC562F4.html

## Example Usages

**Create a virtual switch and bind a port group to it:**

```typescript
import * as pulumi from "@pulumi/pulumi";
import * as vsphere from "@pulumi/vsphere";

const datacenter = pulumi.output(vsphere.getDatacenter({
    name: "dc1",
}, { async: true }));
const esxiHost = datacenter.apply(datacenter => vsphere.getHost({
    datacenterId: datacenter.id,
    name: "esxi1",
}, { async: true }));
const switchHostVirtualSwitch = new vsphere.HostVirtualSwitch("switch", {
    activeNics: ["vmnic0"],
    hostSystemId: esxiHost.id,
    networkAdapters: [
        "vmnic0",
        "vmnic1",
    ],
    standbyNics: ["vmnic1"],
});
const pg = new vsphere.HostPortGroup("pg", {
    hostSystemId: esxiHost.id,
    virtualSwitchName: switchHostVirtualSwitch.name,
});
```

**Create a port group with VLAN set and some overrides:**

This example sets the trunk mode VLAN (`4095`, which passes through all tags)
and sets
[`allow_promiscuous`](https://www.terraform.io/docs/providers/vsphere/r/host_virtual_switch.html#allow_promiscuous)
to ensure that all traffic is seen on the port. The latter setting overrides
the implicit default of `false` set on the virtual switch.

```typescript
import * as pulumi from "@pulumi/pulumi";
import * as vsphere from "@pulumi/vsphere";

const datacenter = pulumi.output(vsphere.getDatacenter({
    name: "dc1",
}, { async: true }));
const esxiHost = datacenter.apply(datacenter => vsphere.getHost({
    datacenterId: datacenter.id,
    name: "esxi1",
}, { async: true }));
const switchHostVirtualSwitch = new vsphere.HostVirtualSwitch("switch", {
    activeNics: ["vmnic0"],
    hostSystemId: esxiHost.id,
    networkAdapters: [
        "vmnic0",
        "vmnic1",
    ],
    standbyNics: ["vmnic1"],
});
const pg = new vsphere.HostPortGroup("pg", {
    allowPromiscuous: true,
    hostSystemId: esxiHost.id,
    virtualSwitchName: switchHostVirtualSwitch.name,
    vlanId: 4095,
});
```

> This content is derived from https://github.com/terraform-providers/terraform-provider-vsphere/blob/master/website/docs/r/host_port_group.html.markdown.



## Create a HostPortGroup Resource

{{< chooser language "javascript,typescript,python,go,csharp" / >}}

{{% choosable language nodejs %}}
<div class="highlight"><pre class="chroma"><code class="language-typescript" data-lang="typescript"><span class="k">new </span><span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/vsphere/#HostPortGroup">HostPortGroup</a></span><span class="p">(</span><span class="nx">name</span>: <span class="nx"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string">string</a></span><span class="p">, </span><span class="nx">args</span>: <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/vsphere/#HostPortGroupArgs">HostPortGroupArgs</a></span><span class="p">, </span><span class="nx">opts</span>?: <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#CustomResourceOptions">pulumi.CustomResourceOptions</a></span><span class="p">);</span></code></pre></div>
{{% /choosable %}}

{{% choosable language python %}}
<div class="highlight"><pre class="chroma"><code class="language-python" data-lang="python"><span class="k">def </span><span class="nf">HostPortGroup</span><span class="p">(resource_name, opts=None, </span>active_nics=None<span class="p">, </span>allow_forged_transmits=None<span class="p">, </span>allow_mac_changes=None<span class="p">, </span>allow_promiscuous=None<span class="p">, </span>check_beacon=None<span class="p">, </span>failback=None<span class="p">, </span>host_system_id=None<span class="p">, </span>name=None<span class="p">, </span>notify_switches=None<span class="p">, </span>shaping_average_bandwidth=None<span class="p">, </span>shaping_burst_size=None<span class="p">, </span>shaping_enabled=None<span class="p">, </span>shaping_peak_bandwidth=None<span class="p">, </span>standby_nics=None<span class="p">, </span>teaming_policy=None<span class="p">, </span>virtual_switch_name=None<span class="p">, </span>vlan_id=None<span class="p">, __props__=None);</span></code></pre></div>
{{% /choosable %}}

{{% choosable language go %}}
<div class="highlight"><pre class="chroma"><code class="language-go" data-lang="go"><span class="k">func </span>NewHostPortGroup<span class="p">(</span><span class="nx">ctx</span> *<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/go/pulumi?tab=doc#Context">pulumi.Context</a></span><span class="p">, </span><span class="nx">name</span> <span class="nx"><a href="https://golang.org/pkg/builtin/#string">string</a></span><span class="p">, </span><span class="nx">args</span> <span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi-vsphere/sdk/go/vsphere/?tab=doc#HostPortGroupArgs">HostPortGroupArgs</a></span><span class="p">, </span><span class="nx">opts</span> ...<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/go/pulumi?tab=doc#ResourceOption">pulumi.ResourceOption</a></span><span class="p">) (*<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi-vsphere/sdk/go/vsphere/?tab=doc#HostPortGroup">HostPortGroup</a></span>, error)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language csharp %}}
<div class="highlight"><pre class="chroma"><code class="language-csharp" data-lang="csharp"><span class="k">public </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi.Vsphere/Pulumi.Vsphere..HostPortGroup.html">HostPortGroup</a></span><span class="p">(</span><span class="nx"><a href="https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types">string</a></span> <span class="nx">name<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi.Vsphere/Pulumi.Vsphere.HostPortGroupArgs.html">HostPortGroupArgs</a></span> <span class="nx">args<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.CustomResourceOptions.html">CustomResourceOptions</a></span>? <span class="nx">opts = null<span class="p">)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language nodejs %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resource.</dd>
    <dt class="property-optional" title="Optional">
        <span>args</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The arguments to use to populate this resource's properties.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

{{% choosable language python %}}
<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resource.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resource.</dd>
    <dt class="property-optional" title="Optional">
        <span>args</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The arguments to use to populate this resource's properties.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

{{% choosable language csharp %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resource.</dd>
    <dt class="property-optional" title="Optional">
        <span>args</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The arguments to use to populate this resource's properties.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

#### Resource Arguments




{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>Active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>Host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>Virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>Active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>Host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>Virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>active_<wbr>nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow_<wbr>forged_<wbr>transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow_<wbr>mac_<wbr>changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow_<wbr>promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>check_<wbr>beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>host_<wbr>system_<wbr>id</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>notify_<wbr>switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>average_<wbr>bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>burst_<wbr>size</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>peak_<wbr>bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>standby_<wbr>nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>teaming_<wbr>policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-required"
            title="Required">
        <span>virtual_<wbr>switch_<wbr>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>vlan_<wbr>id</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}







## HostPortGroup Output Properties

The following output properties are available:




{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span>Active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Computed<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">Dictionary<string, string></span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Host<wbr>Port<wbr>Group<wbr>Ports</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span>Active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Computed<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">map[string]string</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Host<wbr>Port<wbr>Group<wbr>Ports</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>Vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span>active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>computed<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">{[key: string]: string}</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Host<wbr>Port<wbr>Group<wbr>Ports</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-"
            title="">
        <span>active_<wbr>nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>allow_<wbr>forged_<wbr>transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>allow_<wbr>mac_<wbr>changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>allow_<wbr>promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>check_<wbr>beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>computed_<wbr>policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">Dict[str, str]</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>host_<wbr>system_<wbr>id</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>key</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>notify_<wbr>switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Dict[Host<wbr>Port<wbr>Group<wbr>Ports]</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping_<wbr>average_<wbr>bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping_<wbr>burst_<wbr>size</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping_<wbr>enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>shaping_<wbr>peak_<wbr>bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>standby_<wbr>nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>teaming_<wbr>policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>virtual_<wbr>switch_<wbr>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-"
            title="">
        <span>vlan_<wbr>id</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}








## Look up an Existing HostPortGroup Resource

Get an existing HostPortGroup resource's state with the given name, ID, and optional extra properties used to qualify the lookup.

{{< chooser language "javascript,typescript,python,go,csharp  " / >}}

{{% choosable language nodejs %}}
<div class="highlight"><pre class="chroma"><code class="language-typescript" data-lang="typescript"><span class="k">public static </span><span class="nf">get</span><span class="p">(</span><span class="nx">name</span>: <span class="nx"><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/string">string</a></span><span class="p">, </span><span class="nx">id</span>: <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#ID">Input&lt;ID&gt;</a></span><span class="p">, </span><span class="nx">state</span>?: <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/vsphere/#HostPortGroupState">HostPortGroupState</a></span><span class="p">, </span><span class="nx">opts</span>?: <span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/pulumi/#CustomResourceOptions">CustomResourceOptions</a></span><span class="p">): </span><span class="nx"><a href="/docs/reference/pkg/nodejs/pulumi/vsphere/#HostPortGroup">HostPortGroup</a></span></code></pre></div>
{{% /choosable %}}

{{% choosable language python %}}
<div class="highlight"><pre class="chroma"><code class="language-python" data-lang="python"><span class="k">static </span><span class="nf">get</span><span class="p">(resource_name, id, opts=None, </span>active_nics=None<span class="p">, </span>allow_forged_transmits=None<span class="p">, </span>allow_mac_changes=None<span class="p">, </span>allow_promiscuous=None<span class="p">, </span>check_beacon=None<span class="p">, </span>computed_policy=None<span class="p">, </span>failback=None<span class="p">, </span>host_system_id=None<span class="p">, </span>key=None<span class="p">, </span>name=None<span class="p">, </span>notify_switches=None<span class="p">, </span>ports=None<span class="p">, </span>shaping_average_bandwidth=None<span class="p">, </span>shaping_burst_size=None<span class="p">, </span>shaping_enabled=None<span class="p">, </span>shaping_peak_bandwidth=None<span class="p">, </span>standby_nics=None<span class="p">, </span>teaming_policy=None<span class="p">, </span>virtual_switch_name=None<span class="p">, </span>vlan_id=None<span class="p">, __props__=None);</span></code></pre></div>
{{% /choosable %}}

{{% choosable language go %}}
<div class="highlight"><pre class="chroma"><code class="language-go" data-lang="go"><span class="k">func </span>GetHostPortGroup<span class="p">(</span><span class="nx">ctx</span> *<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/go/pulumi?tab=doc#Context">Context</a></span><span class="p">, </span><span class="nx">name</span> <span class="nx"><a href="https://golang.org/pkg/builtin/#string">string</a></span><span class="p">, </span><span class="nx">id</span> <span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/go/pulumi?tab=doc#IDInput">IDInput</a></span><span class="p">, </span><span class="nx">state</span> *<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi-vsphere/sdk/go/vsphere/?tab=doc#HostPortGroupState">HostPortGroupState</a></span><span class="p">, </span><span class="nx">opts</span> ...<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi/sdk/go/pulumi?tab=doc#ResourceOption">ResourceOption</a></span><span class="p">) (*<span class="nx"><a href="https://pkg.go.dev/github.com/pulumi/pulumi-vsphere/sdk/go/vsphere/?tab=doc#HostPortGroup">HostPortGroup</a></span>, error)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language csharp %}}
<div class="highlight"><pre class="chroma"><code class="language-csharp" data-lang="csharp"><span class="k">public static </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi.Vsphere/Pulumi.Vsphere..HostPortGroup.html">HostPortGroup</a></span><span class="nf"> Get</span><span class="p">(</span><span class="nx"><a href="https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/built-in-types">string</a></span> <span class="nx">name<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.Input.html">Input&lt;string&gt;</a></span> <span class="nx">id<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi.Vsphere/Pulumi.Vsphere..HostPortGroupState.html">HostPortGroupState</a></span>? <span class="nx">state<span class="p">, </span><span class="nx"><a href="/docs/reference/pkg/dotnet/Pulumi/Pulumi.CustomResourceOptions.html">CustomResourceOptions</a></span>? <span class="nx">opts = null<span class="p">)</span></code></pre></div>
{{% /choosable %}}

{{% choosable language nodejs %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Required">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>state</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>Any extra arguments used during the lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

{{% choosable language python %}}
<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>resource_name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Optional">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
</dl>
{{% /choosable %}}

{{% choosable language go %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Required">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>state</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>Any extra arguments used during the lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

{{% choosable language csharp %}}

<dl class="resources-properties">
    <dt class="property-required" title="Required">
        <span>name</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The unique name of the resulting resource.</dd>
    <dt class="property-required" title="Required">
        <span>id</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>The <em>unique</em> provider ID of the resource to lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>state</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>Any extra arguments used during the lookup.</dd>
    <dt class="property-optional" title="Optional">
        <span>opts</span>
        <span class="property-indicator"></span>
    </dt>
    <dd>A bag of options that control this resource's behavior.</dd>
</dl>

{{% /choosable %}}

The following state arguments are supported:



{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>Active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Computed<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">Dictionary<string, string>?</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Host<wbr>Port<wbr>Group<wbr>Ports<wbr>Args?</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool?</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">int?</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>Active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Computed<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">map[string]string</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Key</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">*Host<wbr>Port<wbr>Group<wbr>Ports</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">*bool</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">*int</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>active<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow<wbr>Forged<wbr>Transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow<wbr>Mac<wbr>Changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow<wbr>Promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>check<wbr>Beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>computed<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">{[key: string]: string}?</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>host<wbr>System<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>notify<wbr>Switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Host<wbr>Port<wbr>Group<wbr>Ports?</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Average<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Burst<wbr>Size</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">boolean?</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping<wbr>Peak<wbr>Bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>standby<wbr>Nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>teaming<wbr>Policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>virtual<wbr>Switch<wbr>Name</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>vlan<wbr>Id</span>
        <span class="property-indicator"></span>
        <span class="property-type">number?</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>active_<wbr>nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}List of active network adapters used for load balancing.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow_<wbr>forged_<wbr>transmits</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the virtual network adapter is allowed to send network traffic with a different MAC address than
that of its own.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow_<wbr>mac_<wbr>changes</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Controls whether or not the Media Access Control (MAC) address can be changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>allow_<wbr>promiscuous</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable promiscuous mode on the network. This flag indicates whether or not all traffic is seen on a given port.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>check_<wbr>beacon</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable beacon probing. Requires that the vSwitch has been configured to use a beacon. If disabled, link status is used
only.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>computed_<wbr>policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">Dict[str, str]</span>
    </dt>
    <dd>{{% md %}}A map with a full set of the [policy
options][host-vswitch-policy-options] computed from defaults and overrides,
explaining the effective policy for this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>failback</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will re-activate failed interfaces higher in precedence when they come back up.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>host_<wbr>system_<wbr>id</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The [managed object ID][docs-about-morefs] of
the host to set the port group up on. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>key</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name of the port group.  Forces a new resource if
changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>notify_<wbr>switches</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}If true, the teaming policy will notify the broadcast network of a NIC failover, triggering cache updates.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>ports</span>
        <span class="property-indicator"></span>
        <span class="property-type"><a href="#hostportgroupports">Dict[Host<wbr>Port<wbr>Group<wbr>Ports]</a></span>
    </dt>
    <dd>{{% md %}}A list of ports that currently exist and are used on this port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>average_<wbr>bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The average bandwidth in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>burst_<wbr>size</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The maximum burst size allowed in bytes if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>enabled</span>
        <span class="property-indicator"></span>
        <span class="property-type">bool</span>
    </dt>
    <dd>{{% md %}}Enable traffic shaping on this virtual switch or port group.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>shaping_<wbr>peak_<wbr>bandwidth</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The peak bandwidth during bursts in bits per second if traffic shaping is enabled.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>standby_<wbr>nics</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}List of standby network adapters used for failover.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>teaming_<wbr>policy</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The network adapter teaming policy. Can be one of loadbalance_ip, loadbalance_srcmac, loadbalance_srcid, or
failover_explicit.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>virtual_<wbr>switch_<wbr>name</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The name of the virtual switch to bind
this port group to. Forces a new resource if changed.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>vlan_<wbr>id</span>
        <span class="property-indicator"></span>
        <span class="property-type">float</span>
    </dt>
    <dd>{{% md %}}The VLAN ID/trunk mode for this port group.  An ID of
`0` denotes no tagging, an ID of `1`-`4094` tags with the specific ID, and an
ID of `4095` enables trunk mode, allowing the guest to manage its own
tagging. Default: `0`.
{{% /md %}}</dd>

</dl>
{{% /choosable %}}










## Supporting Types

<h4>Host<wbr>Port<wbr>Group<wbr>Ports</h4>
{{% choosable language nodejs %}}
> See the   <a href="/docs/reference/pkg/nodejs/pulumi/vsphere/types/output/#HostPortGroupPorts">output</a> API doc for this type.
{{% /choosable %}}

{{% choosable language go %}}
> See the   <a href="https://pkg.go.dev/github.com/pulumi/pulumi-vsphere/sdk/go/vsphere/?tab=doc#HostPortGroupPortsOutput">output</a> API doc for this type.
{{% /choosable %}}




{{% choosable language csharp %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>Key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Mac<wbr>Addresses</span>
        <span class="property-indicator"></span>
        <span class="property-type">List<string>?</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Type</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language go %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>Key</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Mac<wbr>Addresses</span>
        <span class="property-indicator"></span>
        <span class="property-type">[]string</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>Type</span>
        <span class="property-indicator"></span>
        <span class="property-type">*string</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language nodejs %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>key</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>mac<wbr>Addresses</span>
        <span class="property-indicator"></span>
        <span class="property-type">string[]?</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>type</span>
        <span class="property-indicator"></span>
        <span class="property-type">string?</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

</dl>
{{% /choosable %}}


{{% choosable language python %}}
<dl class="resources-properties">

    <dt class="property-optional"
            title="Optional">
        <span>key</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}The key for this port group as returned from the vSphere API.
{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>mac<wbr>Addresses</span>
        <span class="property-indicator"></span>
        <span class="property-type">List[str]</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

    <dt class="property-optional"
            title="Optional">
        <span>type</span>
        <span class="property-indicator"></span>
        <span class="property-type">str</span>
    </dt>
    <dd>{{% md %}}{{% /md %}}</dd>

</dl>
{{% /choosable %}}









<h3>Package Details</h3>
<dl class="package-details">
	<dt>Repository</dt>
	<dd><a href="https://github.com/pulumi/pulumi-vsphere">https://github.com/pulumi/pulumi-vsphere</a></dd>
	<dt>License</dt>
	<dd>Apache-2.0</dd>
    
</dl>
