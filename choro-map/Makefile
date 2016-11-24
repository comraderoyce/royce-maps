build/laucntycur14.txt:
	mkdir -p $(dir $@)
	curl -o $@ http://www.bls.gov/web/metro/$(notdir $@)

unemployment.tsv:
	cat <(echo "id,rate") \
  		<(tail -n +7 laucntycur14.txt \
  		  | grep 'Aug-16' \
  		  | cut -b 21-22,28-30,129-133 \
  		  | tr -s ' ' \
  		  | dsv2dsv -r ' ') \
  		| csv2tsv \
  		> unemployment.tsv