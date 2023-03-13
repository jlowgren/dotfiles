require "fileutils"
require "yaml"

# Constants
CONFIG_FILE = "config.yml".freeze
OPTION_LINK = "link".freeze

desc "Bootstrap"
task :bootstrap do
  # macOS setup
  system("#{Dir.getwd}/bin/macos") if RUBY_PLATFORM.include? "darwin"

  # Load config
  config = YAML.load_file(CONFIG_FILE)

  config[OPTION_LINK].each do |dest, source|
    puts("Symlink: #{source} -> #{dest}")
    # Create directories wherever necessary
    FileUtils.mkdir_p(File.expand_path(File.dirname(dest)))
    # Create symlinks
    FileUtils.ln_s(File.expand_path(source), File.expand_path(dest), force: true)
  end
end

desc "Install packages"
task :install do
  installers = Dir.glob(File.join(Dir.getwd, "*/install.rb"))

  # Run installation files one directory level down
  installers.each do |f|
    puts("Install: #{installer}")
    installer = File.expand_path(f)
    system(installer)
  end
end
