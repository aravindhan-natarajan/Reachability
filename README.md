# Reachability

Code Snippet for Adding Observer in Base Controller for App:-

    private var reachability : Reachability!

    func observeReachability(){
        guard let reachObj = try? Reachability() else {return}
        self.reachability = reachObj
        NotificationCenter.default.addObserver(self, selector:#selector(self.reachabilityChanged), name: NSNotification.Name.reachabilityChanged, object: nil)
        guard let _ = try? self.reachability.startNotifier() else {return}
    }
    
    func removeObserver() {
        NotificationCenter.default.removeObserver(self, name: NSNotification.Name.reachabilityChanged, object: nil)
    }
    
    @objc func reachabilityChanged(note: Notification) {
        let reachability = note.object as! Reachability
        switch reachability.connection {
        case .unavailable:
            print("Network Unavailable Banner")
        default:
            print("Network Available Banner")
        }
    }
    
    deinit {
        self.removeObserver()
    }
