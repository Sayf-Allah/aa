#Assigning the region based on hostname
function check_region() {
    
    local hostname=$1
    
    # Define the region map
   
    map_json='{
        "iad": "us-ashburn-1",
        "bom": "ap-mumbai-1",
        "frk": "eu-frankfurt-1",
        "icn": "ap-seoul-1",
        "lhr": "uk-london-1",
        "nrt": "ap-tokyo-1",
        "phx": "us-phoenix-1",
        "syd": "ap-sydney-1",
        "yyz": "ca-toronto-1",
        "gru": "sa-saopaulo-1",
        "zrh": "eu-zurich-1",
        "jed": "me-jeddah-1"
    }'

    # Iterate over the JSON key-value pairs
    for key in $(echo "$map_json" | jq -r 'keys[]'); do

        # Check if the hostname contains the key
        if [[ $hostname == *"$key"* ]]; then        
             region=$(echo "$map_json" | jq -r ".$key")
             return
        fi
        
    done

}

# Call the function with the provided hostname
check_region "$hostname"
