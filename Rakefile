desc "Convert all clash CSV files in directory to LZMA"
task :decrypt do 
  dir = ENV["dir"] || "."
  Dir["#{dir}/*.csv"].each do |csv|
    raw = File.binread(csv)
    puts "Decrypting#{csv}..."
    updated_hex = raw.unpack("H*")[0].scan(/.{2}/).insert(9, ["00"]*4).flatten
    File.open("#{File.basename(csv, ".*")}.converted.csv.lzma", "wb") { |f| f.write([updated_hex.join("")].pack("H*")) }
  end
end

desc "Decrypt all LZMA files in directory"
task :uncompress do 
  dir = ENV["dir"] || "."
  Dir["#{dir}/*.lzma"].each do |lzma|
    lxma_executable = ENV["xz_exec"] || "xz"
    system "xz -d #{lzma} --format=lzma"
  end
end

desc "Decrypt and Uncompress all files in directory"
task :shotgun => [:decrypt, :uncompress]
