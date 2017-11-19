# react-interv-project

//UserBadge Component with
//User Profile Image, Name, Number of Followers, Number of people //following
class Userbadge extends React.Component {
 
 render() {
 const {user} = this.props;
 console.log(user);
 return(
  <ul className="user-list">
    <h3>User Details</h3>
    <li>     <img
                className='avatar'
                src={user.avatar_url}
                alt={'avatar for ' + user.login}
              />
            </li>
    <li>{'Name: ' + user.name}</li>
    <li>{'Number of Followers: ' + user.followers}</li>
    <li>{'Following: ' + user.following}</li>
    <h3></h3>
  </ul>
 )
}
}

// 6. Create a Repo List component which will present cards having Repository details.
// Following details should be part of each repository card
// Name, Description, Git URL, Number of Stars, Forks Count, Number of Open Issues, Repository Size
class Repolist extends React.Component {
 render() {
  const {user} = this.props;
  return(
   <div>
     <h3>Repository Details</h3>
     <button onClick={this.userRepos}>Click here</button>
     <ul className="repo-list">
        <li>{'Name: ' + user.name}</li>
        <li>{user.description}</li>
     </ul>
   </div>
  )
 }
}
//// 5. Making an api call to get all the repositories for the user 
// API URL: https://api.github.com/users/{username}/repos




// Search Component
class Search extends React.Component {
constructor(props) {
super(props);

 this.state = {
   user: {},
   repo: []
 };
}

getUser = () => {
 const name = this.refs.name.value;
 fetch(`https://api.github.com/users/${name}`)
   .then(response => response.json())
   .then(data => {
     this.setState({
        user: data
     })
   })
}

userRepos=()=> {
  const name = this.refs.name.value;
  fetch(`https://api.github.com/users/${name}/repos`)
   .then(response => response.json())
   .then(data => {
     this.setState({
        repo: data
     })
   })
}
  render() {
    const {user} = this.state;
    return (
    <div>
      <input type='text' placeholder='github username' ref='name' />
      <button onClick={this.getUser}>Search</button>
      <pre><code>{JSON.stringify(user)}</code></pre>
      <Userbadge user={user}/>
      <Repolist user={user} userRepos={this.userRepos}/>
      
    </div>
    );
  }
}

ReactDOM.render(
  <Search />,
  document.getElementById('container')
);
