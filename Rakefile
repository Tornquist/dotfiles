# encoding: UTF-8

require 'rake'

task :install do
  linkables = Dir['home/*']
  home = Dir.home

  skip_all = false
  overwrite_all = false
  backup_all = false

  if !File.exists?("/bin/zsh")
    puts "✱ Installing zsh"
    `sudo apt-get install zsh`
  end

  if !File.exists?("#{home}/.oh-my-zsh")
    puts "✱ Installing oh-my-zsh"
    `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended`
  end

  puts "\n✱ Symlinking dotfiles"
  linkables.each do |linkable|
    overwrite = false
    backup = false
    linkable = linkable.sub('home/','')
    target = "#{home}/.#{linkable}"

    if File.exists?(target) || File.symlink?(target)
      unless skip_all || overwrite_all || backup_all
        puts "!!! File already exists: #{target}"
        puts "!!! What do you want to do? [s]kip, [S]kip all, [o]verwrite, [O]verwrite all, [b]ackup, [B]ackup all"
        case STDIN.gets.chomp
        when 'o' then overwrite = true
        when 'b' then backup = true
        when 'O' then overwrite_all = true
        when 'B' then backup_all = true
        when 'S' then skip_all = true
        when 's' then next
        end
      end

      FileUtils.rm_rf(target) if overwrite || overwrite_all
      `mv "#{home}/.#{linkable}" "#{home}/backups/.#{linkable}.backup"` if backup || backup_all
    end
    puts "✱ Linked #{target}"
    `ln -s "$PWD/home/#{linkable}" "#{target}"`
  end
end

task :uninstall do
  linkables = Dir.glob('home/*')
  home = Dir.home

  linkables.each do |linkable|
    linkable = linkable.sub('home/','')
    target = "#{home}/.#{linkable}"

    if File.symlink?(target)
      puts "✱ Removed #{target}"
      FileUtils.rm(target)
    end

    if File.exists?("#{home}/.#{linkable}.backup")
      puts "✱ Restored #{linkable}"
      `mv "#{home}/backups/.#{linkable}.backup" "#{home}/.#{linkable}"`
    end
  end
end