# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise32"
  config.ssh.forward_agent = true
  config.vm.provision :chef_solo do |chef|
    chef.data_bags_path = "databags"
    chef.cookbooks_path = ["cookbooks", "site-cookbooks"]

    chef.add_recipe "users::ruby_shadow"
    chef.add_recipe "users::sysadmins"
    chef.add_recipe "users::sysadmin_sudo"

    chef.add_recipe "root_ssh_agent::ppid"
    chef.add_recipe "ssh_known_hosts"

    chef.add_recipe "homesick_agent::data_bag"

    chef.add_recipe "java"
    chef.add_recipe "openfire"

    chef.json = {
      :users => ["yujiorama"],
      :java => {
        :install_flavor => "oracle",
        :oracle => {
          :accept_oracle_download_terms => true
        },
        :jdk_version => "7",
        :jdk => {
          :"7" => {
            :"i586" => {
              :url => 'http://download.oracle.com/otn-pub/java/jdk/7u17-b02/jdk-7u17-linux-i586.tar.gz',
              :checksum => '4046e941e05717538dd4deb1b1f55cb8bb6bd38793c7317034d1f5019086d956'
            }
          }
        },
        :openfire => {
          :database => {
            :type => 'postgresql',
            :password => 'passwd'
          },
          :postgresql => {
            :postgres => 'passwd'
          }
        }
      }
    }
    chef.log_level = :debug
  end
end
