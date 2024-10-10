import UIKit
import AMScrollingNavbar

class ViewController: UIViewController, UITableViewDelegate, UITableViewDataSource {

  @IBOutlet weak var tableView: UITableView!
  
  override func viewDidLoad() {
    super.viewDidLoad()

    // Set up AMScrollingNavbar
    self.scrollingNavbar.showNavbarOnScroll = true // Show navbar on scroll
    self.scrollingNavbar.hideNavbarOnScroll = false // Don't hide navbar on scroll
    self.scrollingNavbar.shouldShowNavigationBarOnPush = true // Show navbar on navigation push

    // Set up table view
    tableView.delegate = self
    tableView.dataSource = self
    tableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
  }

  // UITableViewDataSource methods
  func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return 20 // Number of rows in the table
  }

  func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
    cell.textLabel?.text = "Row (indexPath.row + 1)"
    return cell
  }

  // UITableViewDelegate method
  func scrollViewDidScroll(_ scrollView: UIScrollView) {
    // Update the navbar's alpha based on scroll offset
    let scrollOffset = scrollView.contentOffset.y
    let alpha = min(scrollOffset / 100.0, 1.0) // Adjust the divider for the desired effect
    self.scrollingNavbar.navigationBar.alpha = alpha
  }
}
