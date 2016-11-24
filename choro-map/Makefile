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

build/ne_10m_populated_places.zip:
	curl -o $@ http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_populated_places.zip

build/ne_10m_admin_0_map_subunits.zip:
	curl -o $@ http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_admin_0_map_subunits.zip

build/ne_10m_admin_0_map_subunits.shp: build/ne_10m_admin_0_map_subunits.zip
	unzip -od $(dir $@) $<
	touch $@

build/ne_10m_populated_places.shp: build/ne_10m_populated_places.zip
	unzip -od $(dir $@) $<
	touch $@	

ogr2ogr \
  -f GeoJSON \
  subunits.json \
  ne_10m_admin_0_map_subunits.shp
