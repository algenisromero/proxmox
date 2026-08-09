**1. Removing the enterprise repo**
    - By using the GUI
        Datacenter > [Node Name] > Updates > Repositores
        Select the ones with the word 'enterprise' and disable
        Select add and pick the non-subscription ones
**2. Update & Upgrade**
    - By using the GUI
           Datacenter > [Node Name] > Updates
           Click refresh
           After refresh click upgrade
           Reboot as required
  **3. Remove LVM and use full disk (If just one)**
      - By using GUI
            Go to Datacenter > Storage
            Assign content from 'local-lvm' to 'local' storage
            Remove 'local-lvm'
            Goto Datacenter > [Node Name] > Shell
            Run the following commands
                # lvremove /dev/pbve/data
                # lvresize -l +100%FREE /dev/pve/root
                # resize2fs /dev/mapper/pve-root
  **4. Passthrough (Optional)**
            Goto Datacenter > [Node Name] > Shell
            Run the following commands
              # nano /etc/default/grub
                add the following after the word 'quiet' "intel_iommu=on" (if cpu is intel or amd for amd)
              # update-grub
              # dmesg | grep -e DMAR -e IOMMU
              # dmesg | grep 'remapping'
            Reboot and open BIOS to enable IOMM, look for instructions from your BIOS brand.
            
                
                  
