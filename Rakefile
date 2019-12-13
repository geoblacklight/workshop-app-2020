# Add your own tasks in files placed in lib/tasks ending in .rake,
# for example lib/tasks/capistrano.rake, and they will automatically be available to Rake.

require_relative 'config/application'

Rails.application.load_tasks

require 'solr_wrapper/rake_task' unless Rails.env.production?

namespace :geoblacklight do
  namespace :index do
    desc "Index documents in a directory"
    task :directory, [:directory] => :environment do |_t, args|
      directory = args[:directory]
      docs = Dir[File.join(directory, "*.json")].map { |f| JSON.parse File.read(f) }.flatten
      Blacklight.default_index.connection.add docs
      Blacklight.default_index.connection.commit
    end
  end
end

