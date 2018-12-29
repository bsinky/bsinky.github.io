require 'date'

drafts_dir = '_drafts'
posts_dir  = '_posts'

# rake post['my new post']
desc 'create a new post with "rake post[\'post title\']"'
task :post, :title do |t, args|
  if args.title
    title = args.title
  else
    puts "Please try again. Remember to include the filename."
  end
  mkdir_p "#{posts_dir}"
  filename = "#{posts_dir}/#{Time.now.strftime('%Y-%m-%d')}-#{title.downcase.gsub(/[^\w]+/, '-')}.md"
  puts "Creating new post: #{filename}"
  File.open(filename, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: #{title}
    date: #{Time.new.strftime('%Y-%m-%d')}
    categories: ["misc"]
    tags: ["misc"]
    summary: A new blog post
    comments: true
    pinned: false
    ---

    EOS
  end

# Uncomment the line below if you want the post to automatically open in your default text editor
system ("#{ENV['EDITOR']} #{filename}")
end

# usage: rake draft['my new draft']
desc 'create a new draft post with "rake draft[\'draft title\']"'
task :draft, :title do |t, args|
  if args.title
    title = args.title
  else
    puts "Please try again. Remember to include the filename."
  end
  mkdir_p "#{drafts_dir}"
  filename = "#{drafts_dir}/#{title.downcase.gsub(/[^\w]+/, '-')}.md"
  puts "Creating new draft: #{filename}"
  File.open(filename, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: #{title}
    date: #{Time.new.strftime('%Y-%m-%d')}
    categories: ["misc"]
    tags: ["misc"]
    summary: A new blog post
    comments: true
    pinned: false
    ---

    EOS
  end

# Uncomment the line below if you want the draft to automatically open in your default text editor
system ("#{ENV['EDITOR']} #{filename}")
end

# usage: rake publish['existing draft title']
desc 'publish an existing draft post with "rake publish[\'draft title\']"'
task :publish, :title do |t, args|
  if args.title
    title = args.title
  else
    puts "Please try again. Remember to include the draft title."
  end
  mkdir_p "#{posts_dir}"
  filename = "#{title.downcase.gsub(/[^\w]+/, '-')}.md"
  formatteddate = DateTime.now.strftime("%Y-%m-%d")
  draftfile = "#{drafts_dir}/#{filename}"
  postfilename = "#{posts_dir}/#{formatteddate}-#{filename}"
  puts "Publishing draft: #{postfilename}"
  File.rename(draftfile, postfilename)
  postText = File.read(postfilename)
  newPostText = postText.gsub(/date: [\d]{4}-[\d]{2}-[\d]{2}/, "date: #{formatteddate}")
  File.open(postfilename, "w") { |file| file.puts newPostText }
end

desc 'preview the site with drafts'
task :preview do
  puts "## Generating site"
  puts "## Stop with ^C ( <CTRL>+C )"
  system "bundle exec jekyll serve --watch --drafts"
end

desc 'list tasks'
task :list do
  puts "Tasks: #{(Rake::Task.tasks - [Rake::Task[:list]]).join(', ')}"
  puts "(type rake -T for more detail)\n\n"
end
