## Feature Table View

<table>
    <thead>
        <tr>
            <th>Module</th>
            <th>Platform</th>
            <th>Feature</th>
            <th>0.x.x.x</th>
            <th>1.0.0.0</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan="12">Judger</td>
            <td rowspan="6">Windows 10/11</td>
            <td>File System Write Protection</td>
            <td>Vulnerable</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Privilege / Syscall Whitelisting</td>
            <td>Unssupported</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Process Count Limiting</td>
            <td>Unsupported</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Network Access Control</td>
            <td>Vulnerable</td>
            <td>Rate-Limited</td>
        </tr>
        <tr>
            <td>Resource Limits</td>
            <td>Vulnerable</td>
            <td>Monitored</td>
        </tr>
        <tr>
            <td>Multithreaded Evaluation</td>
            <td>Supported</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td rowspan="6">Linux 3.5+</td>
            <td>File System Write Protection</td>
            <td rowspan="6">Not implemented</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Privilege / Syscall Whitelisting</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Process Count Limiting</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Network Access Control</td>
            <td>Blocked</td>
        </tr>
        <tr>
            <td>Resource Limits</td>
            <td>Enforced</td>
        </tr>
        <tr>
            <td>Multithreaded Evaluation</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td rowspan="14">Middleware</td>
            <td rowspan="14">Windows / Linux</td>
            <td>Account Registration</td>
            <td>Supported</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Account Login</td>
            <td>Supported</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Account Safety Settings (password, name, access flag)</td>
            <td>Partically</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Account Individual Settings (tag, slogan, userpage)</td>
            <td>Unsupported</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Problem Metadata Management</td>
            <td>Partically</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Problem Testcase Management</td>
            <td>Partically</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Contest Management (OI / IOI / ICPC)</td>
            <td>Unsupported</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Record Storage</td>
            <td>Supported</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Record Query (pagination, filtering by uid/pid/cid/language/status)</td>
            <td>Partically</td>
            <td>Planned</td>
        </tr>
        <tr>
            <td>Hack/SelfEval Storage &amp; Query</td>
            <td>Unsupported</td>
            <td>Partically</td>
        </tr>
        <tr>
            <td>Chat Support</td>
            <td>Supported</td>
            <td>Unsupported</td>
        </tr>
        <tr>
            <td>Discussion Support</td>
            <td>Supported</td>
            <td>Unsupported</td>
        </tr>
        <tr>
            <td>File Upload Support (testcase / attachments / etc.)</td>
            <td>Unsupported</td>
            <td>Supported</td>
        </tr>
        <tr>
            <td>Structured Logging (info / warning / error)</td>
            <td>Partically</td>
            <td>Supported</td>
        </tr>
    </tbody>
</table>

## Product Positioning

The 0.x.x.x version series is a technology exploration and validation product, which is unstable and insecure, and is not recommended for use.

The 1.x.x.x version series is a stable release version that is usually safe and efficient, and is recommended for use.

It is worth noting that the 1.x.x.x series is still being implemented and there is currently no available release version.