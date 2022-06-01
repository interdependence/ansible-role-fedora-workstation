# ansible-role-fedora-workstation

An Ansible role to configure [Fedora Workstation].

For configuring the base system: [ansible-role-fedora].

## Requirements

The dconf module depends on the [psutil] Python library (version 4.0.0 and upwards), dconf, dbus-send, and dbus-run-session.

## Role Variables

<table>
<tr>
<th>Variable</th>
<th>Default</th>
<th>Example</th>
</tr>
<tr>
<td>fedora_workstation_configure_flatpak</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_workstation_configure_gnome_extensions</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_workstation_configure_fonts</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_workstation_configure_dconf</td>
<td>true</td>
<td>false</td>
</tr>
<tr>
<td>fedora_workstation_flatpak_remotes</td>
<td>[ ]</td>
<td>

```yaml
fedora_workstation_flatpak_remotes:
  - name: flathub
    state: present
    method: system
    url: https://dl.flathub.org/repo/flathub.flatpakrepo
```

</td>
</tr>
<tr>
<td>fedora_workstation_flatpak_packages</td>
<td>[ ]</td>
<td>

```yaml
fedora_workstation_flatpak_packages:
  # Individual package
  - name: org.mozilla.firefox
    state: present
  # List of packages
  - name: 
      - com.github.tchx84.Flatseal
      - com.ultimaker.cura
    state: present
```

</td>
</tr>
<tr>
<td>fedora_workstation_gnome_extensions</td>
<td>[ ]</td>
<td>

```yaml
fedora_workstation_gnome_extensions:
  - name: just-perfection-desktop@just-perfection
    state: present
```

</td>
</tr>
<tr>
<td>fedora_workstation_fonts</td>
<td>[ ]</td>
<td>

```yaml
fedora_workstation_fonts:
  - name: dejavu-sans-mono-nerd-fonts
    state: present
    url: https://github.com/ryanoasis/nerd-fonts/releases/latest/download/DejaVuSansMono.zip
```

</td>
</tr>
<tr>
<td>fedora_workstation_dconf</td>
<td>{ }</td>
<td>

```yaml
fedora_workstation_dconf:
  /org/gnome/desktop/interface/color-scheme: "'prefer-dark'"
  /org/gnome/desktop/interface/cursor-size: '32'
```

</td>
</tr>
</table>

### Variable Notes

Where `state` is set to `present` in each role variable, the default value is `present`, and can be omitted. If `state` is set to `absent`, the corresponding item will be removed.

## Example Playbook

```yaml
# Configure Fedora Workstation

---

- name: Configure Fedora Workstation
  hosts: workstations
  roles:
    - role: interdependence.fedora-workstation
      vars:
        fedora_workstation_flatpak_remotes:
          - name: flathub
            state: present
            method: system
            url: https://dl.flathub.org/repo/flathub.flatpakrepo
        fedora_workstation_flatpak_packages:
          - name:
              - org.mozilla.firefox
              - com.github.tchx84.Flatseal
              - com.ultimaker.cura
            state: present
        fedora_workstation_gnome_extensions:
          - name: just-perfection-desktop@just-perfection
            state: present
        fedora_workstation_fonts:
          - name: dejavu-sans-mono-nerd-fonts
            state: present
            url: https://github.com/ryanoasis/nerd-fonts/releases/latest/download/DejaVuSansMono.zip
        fedora_workstation_dconf:
          /org/gnome/desktop/interface/color-scheme: "'prefer-dark'"
          /org/gnome/desktop/interface/cursor-size: '32'
```

[Fedora Workstation]: https://getfedora.org/en/workstation/
[ansible-role-fedora]: https://github.com/interdependence/ansible-role-fedora
[psutil]: https://pypi.org/project/psutil/
