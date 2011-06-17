#
# This software is GPL.
#

#######################
#    Version 1.0.0    #
#      not zero       #
#######################
#      SYNOPSIS       #
#######################

require 'symmetric_gpg'

# Files Constructor
files = SymmetricGPG::Files.new('A good passphrase, not this one.')
files.plain = 'README.txt'
files.encrypted = 'README.enc'



exit

# FILES...
# Encript plain file, README.txt, to encripted file, Text.enc.
sgpg.encrypt('README.txt','Text.enc', true) # true means it's OK to overwrite
# Decript encripted file, Text.enc, to decripted file, Text.dec.
sgpg.decrypt('Text.enc','Text.dec', true) # true means it's OK to overwrite
# Text.dec should be identical to README.txt

# STRINGS...
plain = "The rain in spain rains mainly in the plane."
encripted = sgpg.encstr(plain)
puts
puts "Garbled:"
puts encripted # garbled text
puts
decripted = sgpg.decstr(encripted)
puts "Plain:"
puts decripted # "The rain in spain rains mainly in the plane."
puts

# AND IOS...
# plain reader io to encripted writter io
reader = File.open('README.txt','r')
writer = File.open('Text.enc2','w')
# "plain to encripted pipe"
sgpg.p2ep(reader,writer)
writer.close
reader.close
# encripted reader io to plain writter io
reader = File.open('Text.enc2','r')
writer = File.open('Text.dec2','w')
# "encripted to plain pipe"
sgpg.e2pp(reader,writer)
writer.close
reader.close