bodylabs-python-style
=====================


Usage
-----

```rb
$style_version = '1.0.0'

desc "Install style config"
task :install_style_config do
  FileUtils.rm_rf "bodylabs-python-style" if Dir.exists? "bodylabs-python-style"
  raise unless system "git clone https://github.com/bodylabs/bodylabs-python-style.git"
  Dir.chdir 'bodylabs-python-style' do
    raise unless system "git checkout tags/#{$style_config_version}"
  end
end

task :require_style_config do
  Rake::Task[:install_style_config].invoke unless File.executable? 'bodylabs-python-style/bin/pylint_test'
end

task :lint => :require_style_config do
  raise unless system "bodylabs-python-style/bin/pylint_test env_flag --min_rating 10.0"
end
```
